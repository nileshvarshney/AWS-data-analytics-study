## Data Distribution Concept
One node is the leader node, which manages the distribution of data and query processing tasks to the compute nodes. The compute nodes provide resources to do those tasks.

The disk storage for a compute node is divided into a number of slices. The number of slices per node depends on the node size of the cluster. For example, each DS2.XL compute node has two slices, and each DS2.8XL compute node has 16 slices.

### Distribution Goal
- To distribute the workload uniformly among the nodes in the cluster. Uneven distribution, or data distribution skew, forces some nodes to do more work than others, which impairs query performance.

- To minimize data movement as a query runs. If the rows that participate in joins or aggregates are already collocated on the nodes with their joining rows in other tables, the optimizer doesn't need toredistribute as much data when queries run.

### Distribution Style
- AUTO
- EVEN
- KEY
- ALL

## Sort Key
- Compound Sort Key - Might spped up joins, group by, order by and window function
- Interleaved Sort Key - Equal weight to each column, or subset of columns, in the sort key

## COPY command to load data
 - load data from Amazon S3, DynamoDB, text output from remote host.
 - COPY command recommended and much faster than INSERT
 - Data can be encryped before load into S3
 - You can compress the files using gzip, lzop, bzip2 etc.. to save the time

 ```
 -- role-based (recommended)
copy customer from 's3://mybucket/mydata'
iam_role 'arn:aws:iam::12345678901:role/MyRedshiftRole';

-- key-based
copy customer from 's3://mybucket/mydata'
ACCESS_KEY_ID '<access-key-id>'
SECRET_ACCESS_KEY '<secret-access-key>';
 ```

 ### Loading data from Amazon S3
 - Split data file into multiple files
 - Upload files to Amazon S3
 - Run a COPY command
    - Using manifest to specify data files from S3
 - Verify data was loaded correctly

 ```
 -- all files from S3 folder
 copy <table_name> from 's3://<bucket_name>/<object_prefix>'
 authorization
 delimiter '|';

-- from manifest
copy <table_name> from 's3://<bucket_name>/<manifest_file>'
 authorization
 manifest;

 -- compressed
copy customer from 's3://mybucket/customer.lzo'
iam_role 'arn:aws:iam::0123456789012:role/MyRedshiftRole'
delimiter '|' lzop;

-- fixed width 
copy table_name from 's3://mybucket/prefix'
iam_role 'arn:aws:iam::0123456789012:role/MyRedshiftRole'
fixedwidth 'venueid:3,venuename:25,venuecity:12,venuestate:2,venueseats:6';

-- encrypted
copy customer from 's3://mybucket/encrypted/customer'
iam_role 'arn:aws:iam::0123456789012:role/MyRedshiftRole'
master_symmetric_key '<master_key>'
encrypted
delimiter '|';
 ```

 ## Merge Data
 ```
CREATE TEMP TABLE stage (like target);

INSERT INTO stage
SELECT * FROM source
WHERE source.filter = 'filter_expression';

BEGIN TRANSACTION;

DELETE FROM target
USING stage
WHERE target.primarykey = stage.primarykey;

INSERT INTO target
SELECT * FROM stage;

END TRANSACTION;

DROP TABLE stage;
 ```

### Deep copy
A deep copy recreates and repopulates a table by using a bulk insert, which automatically sorts the table. If a table has a large unsorted Region, a deep copy is much faster than a vacuum. The trade off is that you should not make concurrent updates during a deep copy operation.
```
create table likesales (like sales);
insert into likesales (select * from sales);
drop table sales;
alter table likesales rename to sales;
```

## Vacuuming Tables
Amazon Redshift can automatically sort and perform a VACUUM DELETE operation on tables in the background. To clean up tables after a load or a series of incremental updates, you can also run the VACUUM command, either against the entire database or against individual tables.

*Only the table owner or a superuser can effectively vacuum a table.* 

```
select "table", unsorted,vacuum_sort_benefit from svv_table_info order by 1;
```
### Vacuum Type
- VACUUM FULL
- VACUMM DELETE ONLY
- VACUUM SORT ONLY
- VACUUM REINDEX

## unloading data to Amazon S3
- write result serially by adding PARALLEL OFF
- Limit the size of the file by specifying MAXFILESIZE
- Unload automatically encrypt data using SSE-S3
- Max Size of single data file is 6.2GB. Create another file if size exceeds

```
unload ('select * from venue')
to 's3://mybucket/tickit/unload/venue_'
iam_role 'arn:aws:iam::0123456789012:role/MyRedshiftRole';
```

With parallel off and max file size 100 MB
```
unload ('select * from venue')
to 's3://mybucket/tickit/unload/venue_'
iam_role 'arn:aws:iam::0123456789012:role/MyRedshiftRole'
parallel off
maxfilesize 100 mb;
```
using manifest

```
unload ('select * from venue')
to 's3://mybucket/tickit/venue_'
iam_role 'arn:aws:iam::0123456789012:role/MyRedshiftRole'
manifest
allowoverwrite;
```
manifest will look like 
```
{
    "entries": [
        {"url":"s3://mybucket/tickit/venue_0000_part_00"},
        {"url":"s3://mybucket/tickit/venue_0001_part_00"},
        {"url":"s3://mybucket/tickit/venue_0002_part_00"},
        {"url":"s3://mybucket/tickit/venue_0003_part_00"}
    ]
}
```


