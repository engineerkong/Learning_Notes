# Pandas

```
pd.DataFrame({'Yes':[50,21],'No':[131,2]},index)
pd.Series([1,2,3],index=['one','two','three'])
pd.read_csv(xxx,index_col=0)
```

```
book.title = book['title']
reviews.iloc[0, 10] # row_first,columns_second
reviews.loc[0,'country'] # label based selection
reviews.set_index('title')
reviews.loc[reviews.country=='Italy']
reviews.loc[reviews.country.isin(['Italy','France'])]
reviews.loc[reviews.Price.notnull()]
reviews['index_backwards'] = range(len(reviews),0,-1)
```

```
reviews.points.describe()
reviews.points.mean()
reviews.taster_name.unique() / .value_counts()
a: reviews.points.map(lambda p:p-mean)
b: reviews.apply(remean_points,axis='columns')
def remean_points(row):
reviews.country + "_" + reviews.region_1
n_trop = reviews.description.map(lambda desc: "tropical" in desc).sum()
```

```
reviews.groupby("points").points.count()
groupby() - 相同放一块儿
idxmax() - 最大值对应索引
agg() - 跑不同德functions(len,min,max)
reglar index -> multi index
reset_index() - multi index -> regular index
reviews.sort_values(by='len',ascending=False)
reviews.sort_index()
reviews.sort_values(by=['country','len'])
```

```
reviews.price.dtype -> 显示类型
reviews.price.astype('float64') -> 转换类型
reviews[pd.isnull(reviews.country)]
reviews.country,fillna("Unknown")
reviews.country.replace("xx","xxx")
```

```
.rename()
.rename_axis()
concat(), join(), merge()
```
