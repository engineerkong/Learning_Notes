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
