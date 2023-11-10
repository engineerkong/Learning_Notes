# Data Visualization

with **seaborn**

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
