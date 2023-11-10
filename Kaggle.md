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
