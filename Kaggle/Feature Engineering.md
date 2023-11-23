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
