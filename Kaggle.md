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
```

- `LIKE "%xxx%"` 模糊匹配

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
