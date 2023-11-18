# Intro to SQL

**Structured Query Language (SQL)**

- BigQuery

client -> project -> dataset -> tables(shema)

```
from google.cloud import bigquery
client = bigquery.client()
client.dataset
      .get_dataset
      .list_tables
      .list_rows(table,max_results=5).to_dataframe()
      .query
```

- `SELECT`,`FROM`,`WHERE`

```
query = """
        SELECT Name
        FROM 'xxx'
        WHERE Animal='CAT'
        """
```

数据集: ``, 字符串:''

- `GROUPBY`,`HAVING`,`COUNT(),SUM(),AVG(),MIN(),MAX()`

`GROUPBY Animal HAVING COUNT(ID)>1`

Aliasing: ... AS NumPosts

- `ORDER BY Animal DESC`

- `DATE`,`DATETIME`

`SELECT Name, EXTRACT(DAY from Date)`

- `AS`, `WITH` 子数据集

`WITH Seniors AS`
  
- `JOIN` 合并数据集

```
FROM xxx INNER JOIN xxx ON # 必须满足
         LEFT  JOIN        # 返回左，即使无右
         RIGHT JOIN        # 返回右，即使无左
         FULL JOIN         # 全包含
```

必须添加 `ON` 选择条件

- `LIKE "%xxx%"` 模糊匹配

# Advanced SQL

- `UNION` # verticallly concatenate

`UNION ALL` # 同时存在, `UNION DISTINCT` # 合并重复

```
union_query = """
              SELECT c.by
              FROM `bigquery-public-data.hacker_news.comments` AS c
              WHERE EXTRACT(DATE FROM c.time_ts) = '2014-01-01'
              UNION DISTINCT
              SELECT s.by
              FROM `bigquery-public-data.hacker_news.stories` AS s
              WHERE EXTRACT(DATE FROM s.time_ts) = '2014-01-01'
              """
```

- Analytic Functions

```
SELECT *,
    SUM(num_trips) 
        OVER (
             ORDER BY trip_date
             ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
             ) AS cumulative_trips
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
```
1. Analytic aggregate functions:

`MIN()`, `MAX()`, `AVG()`, `SUM()`, `COUNT()`

2. Analytic navigation functions:

`FIRST_VALUE()`, `LAST_VALUE()`

`LEAD()` # 后一行数据, `LAG()` # 前一行数据

3. Analytic numbering functions:

`ROW_NUMBER()`, `RANK()` # 排序

- nested and repeated data

nested: (Name:McFly,Type:Frisbee) - RECORD STRUCT 数据

`Toy.Name` and `Toy.Type`

repeated: [Frisbee,Bone,Rope] - REPEATED ARRAY 数据

`UNNEST(Toys) AS Toy_Type` # 解除 nested and repeated

- Efficient Queries

`show_amount_of_data_scanned()` shows the amount of data the query uses.

`show_time_to_run()` prints how long it takes for the query to execute.

1. Only select the columns you want.

2. Read less data.

3. Avoid N:N JOINs

# Data Visualization

with **seaborn**

![LPWH19I](https://github.com/engineerkong/Learning_Notes/assets/89781823/c5ea8a6c-4337-49f1-9aed-34eec2125011)

`ign_data = pd.read_csv(ign_filepath, index_col="Platform")`

`sns.lineplot(data=spotify_data)`

`sns.lineplot(data=spotify_data['Shape of You'], label="Shape of You")`

`sns.barplot(x=flight_data.index, y=flight_data['NK'])`

`sns.heatmap(data=flight_data, annot=True)`

`sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'], hue=insurance_data['smoker'])`

`sns.regplot(x=insurance_data['bmi'], y=insurance_data['charges']) # regression line`

`sns.lmplot(x="bmi", y="charges", hue="smoker", data=insurance_data) # with seperate regression lines for hues`

`sns.swarmplot(x=insurance_data['smoker'], y=insurance_data['charges']) # cartegorical scatter plot`

`sns.histplot(data=iris_data, x='Petal Length (cm)', hue='Species') # histogramm`

`sns.kdeplot(data=iris_data['Petal Length (cm)'], shade=True) # density plot`

`sns.jointplot(x=iris_data['Petal Length (cm)'], y=iris_data['Sepal Width (cm)'], kind="kde") # 2D KDE(kernel density estimate) plot`

`list(spotify_data.columns)`

`sns.set_style("dark") # (1)"darkgrid", (2)"whitegrid", (3)"dark", (4)"white", and (5)"ticks"`

# Feature Engineering

The **mutual information (MI)** between two quantities is a measure of the extent to which knowledge of one quantity reduces uncertainty about the other.

```
for colname in X.select_dtypes("object"):

    X[colname], _ = X[colname].factorize()

discrete_features = X.dtypes == int

def make_mi_scores(X, y, discrete_features):

    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features)
    
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    
    mi_scores = mi_scores.sort_values(ascending=False)
    
    return mi_scores
```

Relationships among numerical features are often expressed through **mathematical formulas**.

`autos["stroke_ratio"] = autos.stroke / autos.bore`

**Building-Up and Breaking-Down Features**: (999) 555-0123

`customer[["Type", "Level"]] = (customer["Policy"].str.split(" ", expand=True))`

**Group transforms**, which aggregate information across multiple rows grouped by some category.

`customer["AverageIncome"] = (customer.groupby("State")["Income"].transform("mean"))`

```
# One-hot encode Categorical feature, adding a column prefix "Cat"
X_new = pd.get_dummies(df.Categorical, prefix="Cat")

# Multiply row-by-row
X_new = X_new.mul(df.Continuous, axis=0)

# Join the new features to the feature set
X = X.join(X_new)
```

```
X_3["PorchTypes"] = df[[
    "WoodDeckSF",
    "OpenPorchSF",
    "EnclosedPorch",
    "Threeseasonporch",
    "ScreenPorch",
]].gt(0.0).sum(axis=1)
```

```
X_4["MSClass"] = df.MSSubClass.str.split("_",n=1,expand=True)[0]
```

**K-means Clustering** for unsupervised learning:

1 assign points to the nearest cluster centroid

2 move each centroid to minimize the distance to its points

```
kmeans = KMeans(n_clusters=10, n_init=10, random_state=0)
X["Cluster"] = kmeans.fit_predict(X_scaled) # 每个样本所属的簇
X_cd = kmeans.fit_transform(X_scaled) # 转换后的数据
```

**principal component analysis (PCA)** is a great tool to help you discover important relationships in the data and can also be used to create more informative features. It makes this precise through each component's **percent of explained variance**.

```
pca = PCA()
X_pca = pca.fit_transform(X_scaled)
plot_variance(pca)
mi_scores = make_mi_scores(X_pca, y, discrete_features=False) # mutual information
```

A **target encoding** is any kind of encoding that replaces a feature's categories with some number derived from the target:

MEstimateEncoder 旨在通过考虑类别的频率和目标变量的概率来更好地编码类别型特征，以提高机器学习模型的性能

`autos["make_encoded"] = autos.groupby("make")["price"].transform("mean")`

```
encoder = MEstimateEncoder(cols=["Zipcode"], m=5.0)
encoder.fit(X_encode, y_encode)
X_train = encoder.transform(X_pretrain)
```

**smoothing** is to blend the in-category average with the overall average. Rare categories get less weight on their category average, while missing categories just get the overall average:

`encoding = weight * in_category + (1 - weight) * overall`

# Intro to Deep Learning

- A Single Neuron

![mfOlDR6](https://github.com/engineerkong/Learning_Notes/assets/89781823/486e044a-c90d-4f7d-84b1-a542074c3a3d)

Deep learning is an approach to machine learning characterized by deep stacks of computations.


Keras:

```
from tensorflow import keras
from tensorflow.keras import layers
# Create a network with 1 linear unit
model = keras.Sequential([
    layers.Dense(units=1, input_shape=[3])
])
w, b = model.weights
```

- Deep Neural Networks

modularity - building up a complex network from simpler functional units.

dense layers - collect together linear units having a common set of inputs. `layers.Dense(units=4,activation='relu),input_shape=[2]`

convolutional layers / recurrent layers

activation function: `layers.Activation('relu')` # ReLU: max(0,x) make nonlinear, except the output layer other: elu, selu, swish

```
from tensorflow import keras
from tensorflow.keras import layers
model = keras.Sequential([
    # the hidden ReLU layers
    layers.Dense(units=4, activation='relu', input_shape=[2]),
    layers.Dense(units=3, activation='relu'),
    # the linear output layer 
    layers.Dense(units=1),
])
```

- Stochastic Gradient Descent

**Loss function** 

loss function: mean absolute error (MAE) - abs(y_true-y_pred)

learning rate: optimizer - stochastic gradient descent / adam

size of batch: each iteration (epoch) 's sample of training data

```
model.compile(
    optimizer="adam",
    loss="mae",
)
```

```
history = model.fit(
    X_train, y_train,
    validation_data=(X_valid, y_valid),
    batch_size=256,
    epochs=10,
)
```

- Overfitting and Underfitting

1. signal and noise
training loss goes down: learn signal or noise

validation loss goes down: learn signal

2. capacity (how many neurons it has and how they are connected together)

underfitting: not enough signal, increase capacity (wider or deeper)

overfitting: too much noise

3. early stopping

![eP0gppr](https://github.com/engineerkong/Learning_Notes/assets/89781823/23973fe6-423a-41b9-9df0-617ec10c39a7)

callback: a function you want run every so often while the network trains.

```
early_stopping = EarlyStopping(
    min_delta=0.001, # minimium amount of change to count as an improvement
    patience=20, # how many epochs to wait before stopping
    restore_best_weights=True,
)
```
- Dropout and Batch Normalization

dropout layer: randomly drop out some fraction of a layer's input units every step of training - correct overfitting

```
keras.Sequential([
    # ...
    layers.Dropout(rate=0.3), # apply 30% dropout to the next layer
    layers.Dense(16),
    # ...
])
```

batch normalization layer: normalize the data before it goes into the network - speed up optimization

```
keras.Sequential([
    # ...
    layers.Dense(16),
    layers.BatchNormalization(),
    layers.Activation('relu'),
    # ...
])
```

```
    layers.Dense(1024, activation='relu'),
    layers.Dropout(0.3),
    layers.BatchNormalization(),
    layers.Dense(1),
```

- Binary Classification

accuracy = number_correct / total, threshold

cross-entropy: H(P,Q) = −∑P(x)logQ(x)

```
model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['binary_accuracy'],
)
```

sigmoid activation: sigmoid(x) = 1/(1+e^(-x)) # for binary classification

`layers.Dense(1, activation='sigmoid')` # output layer use sigmoid activation 

# Computer Vision

- Convolution (filter) + Activation (detect) + Maximum Pooling (condense)

pretrained base + untrained head

Problem: Translation Invariance - pooling destroyed some of their positional information

```
model = keras.Sequential([
    layers.Conv2D(filters=64, kernel_size=3), # activation is None
    layers.MaxPool2D(pool_size=2), / layers.GlobalAvgPool2D(), # reduces each of features to a single value
    # More layers follow
])
```

```
image_condense = tf.nn.pool(
    input=image_detect, # image in the Detect step above
    window_shape=(2, 2),
    pooling_type='MAX',
    # we'll see what these do in the next lesson!
    strides=(2, 2),
    padding='SAME',
)
```

- The sliding window:

The **strides** parameter says how far the window should move at each step, like (1,1)
 
and the **padding** parameter describes how we handle the pixels at the edges of the input. like 'valid' or 'same'

The receptive field just tells you which parts of the input image a neuron receives information from.

```
image = circle_64
kernel = bottom_sobel
visiontools.show_extraction(
    image, kernel,
    conv_stride=1,
    conv_padding='valid',
    pool_size=2,
    pool_stride=2,
    pool_padding='same',
    
    subplot_shape=(1, 4),
    figsize=(14, 6),
)
```

one-dimensional convolution

- Custom Convnets

Convolutional Blocks: convolution - activation - pooling

- Data Argumentation

train on more data: add in some extra fake data that looks reasonably like the real data and your classifier will improve, like flipped

```
model = keras.Sequential([
    # Preprocessing
    preprocessing.RandomFlip('horizontal'), # flip left-to-right
    preprocessing.RandomContrast(0.5), # contrast change by up to 50%
    # Base
    pretrained_base,
    # Head
    layers.Flatten(),
    layers.Dense(6, activation='relu'),
    layers.Dense(1, activation='sigmoid'),
])
```

```
augment = keras.Sequential([
    # preprocessing.RandomContrast(factor=0.5),
    preprocessing.RandomFlip(mode='horizontal'), # meaning, left-to-right
    # preprocessing.RandomFlip(mode='vertical'), # meaning, top-to-bottom
    # preprocessing.RandomWidth(factor=0.15), # horizontal stretch
    # preprocessing.RandomRotation(factor=0.20),
    # preprocessing.RandomTranslation(height_factor=0.1, width_factor=0.1),
])
```

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

# Data Cleaning

- Handling Missing Values

```
# get the number of missing data points per column
missing_values_count = nfl_data.isnull().sum()
# look at the # of missing points in the first ten columns
missing_values_count[0:10]

# how many total missing values do we have?
total_cells = np.product(nfl_data.shape)
total_missing = missing_values_count.sum()
# percent of data that is missing
percent_missing = (total_missing/total_cells) * 100
print(percent_missing)
```

drop or fill?

```
# remove all columns with at least one missing value
columns_with_na_dropped = nfl_data.dropna(axis=1)
columns_with_na_dropped.head()

# replace all NA's the value that comes directly after it in the same column, 
# then replace all the remaining na's with 0
subset_nfl_data.fillna(method='bfill', axis=0).fillna(0)
```

- Scaling and Normalization

in **scaling**, you're changing the range of your data, while

```
# mix-max scale the data between 0 and 1
scaled_data = minmax_scaling(original_data, columns=[0])
```

in **normalization**, you're changing the shape of the distribution of your data.

```
# normalize the exponential data with boxcox
normalized_data = stats.boxcox(original_data)
```

- Parsing Dates

```
# create a new column, date_parsed, with the parsed dates
landslides['date_parsed'] = pd.to_datetime(landslides['date'], format="%m/%d/%y")
# or
landslides['date_parsed'] = pd.to_datetime(landslides['Date'], infer_datetime_format=True)
# get the day of the month from the date_parsed column
day_of_month_landslides = landslides['date_parsed'].dt.day
```

- Character Encodings

```
after = before.encode("utf-8", errors="replace")
after.decode("utf-8")
```

```
# try to read in a file not in UTF-8
kickstarter_2016 = pd.read_csv("../input/kickstarter-projects/ks-projects-201612.csv")
# look at the first ten thousand bytes to guess the character encoding
with open("../input/kickstarter-projects/ks-projects-201801.csv", 'rb') as rawdata:
    result = charset_normalizer.detect(rawdata.read(10000))
# check what the character encoding might be
print(result)
# read in the file with the encoding detected by charset_normalizer
kickstarter_2016 = pd.read_csv("../input/kickstarter-projects/ks-projects-201612.csv", encoding='Windows-1252')
# save our file (will be saved as UTF-8 by default!)
kickstarter_2016.to_csv("ks-projects-201801-utf8.csv")
```

- Inconsistent Data Entry

' Germany', and 'germany'

```
matches = fuzzywuzzy.process.extract("south korea", countries, limit=10, scorer=fuzzywuzzy.fuzz.token_sort_ratio) # fuzzywuzzy 查找工具
```

```
def replace_matches_in_column(df, column, string_to_match, min_ratio = 47):
    # get a list of unique strings
    strings = df[column].unique()  
    # get the top 10 closest matches to our input string
    matches = fuzzywuzzy.process.extract(string_to_match, strings, 
                                         limit=10, scorer=fuzzywuzzy.fuzz.token_sort_ratio)
    # only get matches with a ratio > 90
    close_matches = [matches[0] for matches in matches if matches[1] >= min_ratio]
    # get the rows of all the close matches in our dataframe
    rows_with_matches = df[column].isin(close_matches)
    # replace all rows with close matches with the input matches 
    df.loc[rows_with_matches, column] = string_to_match   
    # let us know the function's done
    print("All done!")

replace_matches_in_column(df=professors, column='Country', string_to_match="south korea")
```

# Intro to AI Ethics

- In the **human-centered design** lesson, you’ll learn how to design an AI system to ensure that it serves the needs of the people that it is intended for.
6 Steps:
  
1. Understand people's needs to define the problem
2. Ask if AI adds value to any potential solution
3. Consider the potential harms that the AI system could cause
4. Prototype, starting with non-AI solutions
5. Provide ways for people to challenge the system
6. Build in safety measures

- In the **bias** lesson, you’ll determine how AI systems can learn to discriminate against certain groups.

Bias refers to negative, unwanted consequences of ML applications, especially if the consequences disproportionately affect certain groups.

6 Types of bias:

1. Historical bias occurs when the state of the world in which the data was generated is flawed.
2. Representation bias occurs when building datasets for training a model, if those datasets poorly represent the people that the model will serve.
3. Measurement bias occurs when the accuracy of the data varies across groups.
4. Aggregation bias occurs when groups are inappropriately combined, resulting in a model that does not perform well for any group or only performs well for the majority group.
5. Evaluation bias occurs when evaluating a model, if the benchmark data does not represent the population that the model will serve.
6. Deployment bias occurs when the problem the model is intended to solve is different from the way it is actually used.

In the **fairness** lesson, you’ll learn to quantify the extent of the bias in AI systems.

4 fairness criteria: 

1. Demographic parity / statistical parity: Demographic parity says the model is fair if the composition of people who are selected by the model matches the group membership percentages of the applicants.
2. Equal opportunity: Equal opportunity fairness ensures that the proportion of people who should be selected by the model ("positives") that are correctly selected by the model is the same for each group.
3. Equal opportunity: That is, the percentage of correct classifications should be the same for each group.
4. Group unaware:removes all group membership information from the dataset.

confusion matrix - Sensitivity / True positive rate
In the **model cards** lesson, you’ll learn how to use a popular framework for improving public accountability for AI models.
