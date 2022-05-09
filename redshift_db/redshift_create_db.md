### Create database
```
create database ticket;
```

### Create users
```
CREATE USER guest PASSWORD 'Abcd1234';
```

### Drop user
```
DROP USER guest;
```

### Create table
```
CREATE TABLE test_table(testcol int);
SELECT * FROM pg_table_def WHERE tablename = 'test_table';
INSERT into test_table VALUES(100);
```

 ### Notes
- encoding, distkey, and sortkey columns are used by for parallel processing.
- STL views for logging
- STV table for snapshot data
- SVV & SVL System view
- PG system catalog table

### Cancel a query
Get pid from stv_recent of running query(status = 'Running')
```
cancel 18764;
```
### Cancel query using the superuser queue
```
set query_group to 'superuser';
cancel 18764;
reset query_group;
```

### Automatic table optimization

```
-- Auto 
ALTER TABLE table_name ALTER SORTKEY AUTO;
ALTER TABLE table_name ALTER DISTSTYLE AUTO;

-- Even
ALTER TABLE table_name ALTER DISTSTYLE EVEN;

-- ALL
ALTER TABLE table_name ALTER DISTSTYLE ALL;

-- Distkey
ALTER TABLE table_name ALTER DISTSTYLE KEY DISTKEY c1;

-- sort key
ALTER TABLE table_name ALTER SORTKEY(c1, c2));
ALTER TABLE table_name ALTER SORTKEY NONE;

-- compression
ALTER TABLE table-name ADD [ COLUMN ] column_name column_type ENCODE encoding-type;

```
## Create and populate encoded table

```
CREATE TABLE encodingvenue (
    venueraw varchar(100) encode raw,
    venuebytedict varchar(100) encode bytedict,
    venuelzo varchar(100) encode lzo,
    venuerunlength varchar(100) encode runlength,
    venuetext255 varchar(100) encode text255,
    venuetext32k varchar(100) encode text32k,
    venuezstd varchar(100) encode zstd
    );

INSERT INTO encodingvenue
SELECT 
    venuename as venueraw, 
    venuename as venuebytedict, 
    venuename as venuelzo,
    venuename as venuerunlength, 
    venuename as venuetext32k, 
    venuename as venuetext255,
    venuename as venuezstd
FROM cartesian_venue;  
```
