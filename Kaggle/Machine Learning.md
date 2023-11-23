# Intro to Machine Learning

- Decision Tree

```
from sklearn.tree import DecisionTreeRegressor
model = DecisionTreeRegressor(random_state=1)
```

- pandas.DataFrame 多列 .Series 单列

```
pandas.read_csv()
home_data.describe()
```

- sklearn

1 Define 2 Fit 3 Predict 4 Evaluate

- Model Validation

predictive accuracy: Mean Absolute Error (MAE)

sklearn.model_selection -> train_test_split

sklearn.metrics -> mean_absolute_error

- Underfitting, Overfitting

Underfitting: not enough training

Overfitting: too much divided

- Random Forests

```
from sklearn.ensemble import RandomForestRegressor
```

# Intermediate Machine Learning

- missing values, categorical variables

1. drop columns with missing values

```
X.drop(cols_with_missing,axis=1)
```

2. imputation 插值

```
my_imputer = SimplerImputer()
imputed_X_train = pd.DataFrame(my_impute.fit_transform())
imputed_X_train.columns = X_train.columns
```

3. an extension to imputation

```
X_train_plus[col+'_was_missing'] = X_train_plus[cols].isnull()
```

- Categorical variable

categorical variable: takes only a limited number of values - (never, rarely, most days, every day)

1. Drop Categorical Variable

```
drop_X_train = X_train.select_dtypes(exclude=['object'])
```

2. Ordinal Encoding

```
ordinal_encoder = OrdinalEncoder()
label_X_train[object_cols] = ordinal_encoder.fit_transform(X_train[object_cols])
```

3. One-Hot Encoding (nominal variables)

```
OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse = False)
```

- Pipelines

Step 1: Define Preprocessing Steps

numerical_transformer / categorical_transformer -> preprocessor

Step 2: Define the model

Step 3: Create and evaluate the pipline

```
my_pipeline = Pipeline(steps=[('preprocessor', ...),('model',...)])
```

- Cross-Validation

run modeling process on different subsets of the data to get multiple measures of model quality

```
scores = -1*cross_val - score(my_pipeline,X,y,cv=5,scoring='neg_mean_absolute_error')
```

GridSearch to search best combi of hps

- XGBoost

gradient boosting - ensemble method (cycles)

naive model -> make predictions -> calculate loss -> train new model -> add new model to ensemble -> make predictions -> ...

```
from xgboost import XGBRegressor
my_model = XGBRegressor
```

hps: 1 n_estimators 2 early_stopping_rounds 3 learning_rate 4 n_jobs

- target leakage 数据在预测后

train-test contamination: 数据不同于实际 (after remissing)
