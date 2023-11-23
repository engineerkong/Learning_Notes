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
