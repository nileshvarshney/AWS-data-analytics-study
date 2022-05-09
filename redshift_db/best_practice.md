### Redshift Best Practice
Massively parallel processing, columnar data compression and columnar data storage.

### Best Practice for designing tables
**Choose best sort key:** 
- When use automatic table optimization, you don't need to choose the sort key of the table.
- if recent data is queries most frequently, specify timestamp column for the sort key.
- if you do frequent range filtering or equality on one column, specify that column as a sort key.
- if you frequently join a table, specify join column as both sort key and distribution key.

**Choose best distibution style:**
-  Distribute the fact table and one dimension table on their common column.
- Choose the largest dimension based on the size of the filtered dataset.
- Choose a column with high cardinality in teh filtered result set.
- Change some dimension tables to use ALL distribution - distributing the entire tables to all of the nodes.

**Let Copy choose compression encloding:**

In most cases automatic compression produce the best results. in balance oberall performance.

**Define Primary key and foreign Key Constraints:** 

Do not define primary key and foreign key constraints unless your application enforces the constraints. Amazon Redshift doees not enforce unique, primary and foreign key constraints.

**Use the smallest possible column size:**

**Use date/time data type for date columns:**
Redshift stores DATE and TIMESTAMP data more effectively than CHAR or VARCHAR. Which result better query performance.

### Best Practice for loading data

- Use COPY command to load data
- Use a single COPY command to load from multiple files
- Split your load data into multiple files (splited file size equal, between 1MB and 1 GB after compression)
- compress your data files
```
copy time
from 's3://mybucket/data/timerows.lzo'
iam_role 'arn:aws:iam::0123456789012:role/MyRedshiftRole'
lzop
delimiter '|';
```

- Verify data file before and after a load (before load in S3 and after load in STL_LOAD_COMMITS)

- Use a multi-row insert
```
insert into category_stage values
(default, default, default, default),
(20, default, 'Country', default),
(21, 'Concerts', 'Rock', default);
```
- Use a Bulk insert
```
insert into category_stage
(select * from category);

creat table category_stage as
select * from category;
```
- Load data in sort key order to avoid needing to vacuum
- Load data in sequential blocks according to sort order to eliminate the need to vacumm
- Use time-series tables: if your table has fixed retention period, you can organize data as a sequence of time series tables(each table is identical but contain data for differernt time ranges)
- Use staging table to perform a merge (upsert) - redshift does not supprt merge statement

**Best practice for designing Query**
- Avoid SELECT *. Include only the columns required
- Use Case expression to perform complex aggregation and avoid the same table multiple time
- Don't use cross join unless absolutely necessary
- Use sub-query in case where one table in the query is used only for the predicte condition and return small number of rows(less than 200)
- Use predicate to restrict dataset as much as possible
- In predicate use least expensive operation
- avoid using functions in query predicates
- Add predicte top filter tables that participated in joins.
- Use sort key in the GROUP BY clause.
- if you use both GROUP BY and ORDER BY clause , make sure that you put the columns in the same order in both.