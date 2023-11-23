# Time Series

- Linear Regression with Time Series

The basic object of forecasting is the time series, which is a set of observations recorded over time.

time-step features and lag features: using either time-step or lag as the x-axis

```
time = np.arange(len(df.index))  # time dummy
df['time'] = time
lag_1 = df['sales'].shift(1)
df['lag_1'] = lag_1
X = df.loc[:, ['time']]  # features
y = df.loc[:, 'sales']  # target
```

- Trend

The trend component of a time series represents a persistent, long-term change in the mean of the series.

Moving Average Plots: average of a period

linear trend: target = a * time + b

quadratic trend: target = a * time ** 2 + b * time + c

```
moving_average = tunnel.rolling(
    window=365,       # 365-day window
    center=True,      # puts the average at the center of the window
    min_periods=183,  # choose about half the window size
).mean()              # compute the mean (could also do median, std, min, max, ...)
```

```
dp = DeterministicProcess(
    index=tunnel.index,  # dates from the training data
    constant=True,       # dummy feature for the bias (y_intercept)
    order=1,             # the time dummy (trend)
    drop=True,           # drop terms if necessary to avoid collinearity
)
X = dp.in_sample()
X = dp.out_of_sample(steps=30)
```

- Seasonality

We say that a time series exhibits seasonality whenever there is a regular, periodic change in the mean of the series.

The first kind, indicators, is best for a season with few observations, like a weekly season of daily observations. 

The second kind, Fourier features, is best for a season with many observations, like an annual season of daily observations.

```
# days within a week
X["day"] = X.index.dayofweek  # the x-axis (freq)
X["week"] = X.index.week  # the seasonal period (period)
# days within a year
X["dayofyear"] = X.index.dayofyear
X["year"] = X.index.year
```

```
fourier = CalendarFourier(freq="A", order=10)  # 10 sin/cos pairs for "A"nnual seasonality
dp = DeterministicProcess(
    index=tunnel.index,
    constant=True,               # dummy feature for bias (y-intercept)
    order=1,                     # trend (order 1 means linear)
    seasonal=True,               # weekly seasonality (indicators)
    additional_terms=[fourier],  # annual seasonality (fourier)
    drop=True,                   # drop terms to avoid collinearity
)
```

- Time Series as Features

cycles - depend on the recent past, using lag plot

- Hybrid Models

linear regression + XGBoost hybrid

series = trend + seasons + cycles + error

error (residuals): the difference between the actual curve and the fitted curve

```
# 1. Train and predict with first model
model_1.fit(X_train_1, y_train)
y_pred_1 = model_1.predict(X_train)
# 2. Train and predict with second model on residuals
model_2.fit(X_train_2, y_train - y_pred_1)
y_pred_2 = model_2.predict(X_train_2)
# 3. Add to get overall predictions
y_pred = y_pred_1 + y_pred_2
```

```
def fit(self, X_1, X_2, y):
    # YOUR CODE HERE: fit self.model_1
    self.model_1.fit(X_1,y)

    y_fit = pd.DataFrame(
        # YOUR CODE HERE: make predictions with self.model_1
        self.model_1.predict(X_1),
        index=X_1.index, columns=y.columns,
    )
    # YOUR CODE HERE: compute residuals
    y_resid = y - y_fit
    y_resid = y_resid.stack().squeeze() # wide to long
    # YOUR CODE HERE: fit self.model_2 on residuals
    self.model_2.fit(X_2, y_resid)
    # Save column names for predict method
    self.y_columns = y.columns
    # Save data for question checking
    self.y_fit = y_fit
    self.y_resid = y_resid
```

```
def predict(self, X_1, X_2):
    y_pred = pd.DataFrame(
        # YOUR CODE HERE: predict with self.model_1
        self.model_1.predict(X_1),
        index=X_1.index, columns=self.y_columns,
    )
    y_pred = y_pred.stack().squeeze()  # wide to long
    # YOUR CODE HERE: add self.model_2 predictions to y_pred
    y_pred += self.model_2.predict(X_2)
    return y_pred.unstack()  # long to wide
```

```
model = BoostedHybrid(
    model_1=LinearRegression(),
    model_2=XGBRegressor(),
)
model.fit(X_1, X_2, y)
y_pred = model.predict(X_1,X_2)
y_pred = y_pred.clip(0.0)
```

- Forecasting with Machine Learning

```
y = family_sales.loc[:, 'sales']
# Make 4 lag features
X = make_lags(y, lags=4).dropna()
# Make multistep target
y = make_multistep_target(y, steps=16).dropna()
y, X = y.align(X, join='inner', axis=0)
model = RegressorChain(base_estimator=XGBRegressor())
```
