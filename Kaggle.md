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
