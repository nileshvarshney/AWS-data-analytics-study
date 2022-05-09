## Athena
Interactive query service for analyzing s3 data using standard sql. Serverless service. Amazon Athena uses Presto with full standard SQL support. Pay per Query.Create athena table with Glue Crawler.

Supports:
- csv, tsv, json and text(human readable)
- ORC, Parquet, AVRO (columnar, splitable)
- Compression such as gzip, lzo, snappy etc.
- process unstructured, semi-structured, and structured data sets
- supported data types INTEGER, DOUBLE, VARCHAR, MAPS, ARRAY and STRUCT.
- Amazon Athena uses **SerDes** to interpret the data read from Amazon S3

### Ideal Pattern
- Interactive ad hoc querying for weblogs
- Interactive Analytical Solutions with notebook-based solutions
- Analyze AWS service logs (Cloud Trail, Cloud Front, VPC and other logs in S3)
- Query staging data before loading into Amazon Redshift

### Anti Pattern 
- Enterprise Reporting and Business Intelligence Workloads(Redshift is better option)
- ETL workload(Amazon EMR/AWS Glue is better option with large dataset)
- RDBBS (RDS is better option) 

### Perfromace
You can improve the performance of your query by **compressing, partitioning, and converting your data into columnar formats**. This means Athena can scan less data from Amazon S3 when executing your query.

### Durability and availability
Amazon Athena is highly available and executes queries using compute resources across multiple facilities, automatically routing queries appropriately if a particular facility is unreachable. 

Because Athena uses Amazon S3 as its underlying data store, you get Amazon S3 durability (99.999999999%) of objects. Data is redundantly stored across multiple facilities and multiple devices in each facility.

### Scalability and elasticity
Athena is serverless, so there is no infrastructure to set up or manage, and it can scale automatically, as needed.

### Interfaces
Querying can be done using the Athena Console. You can connect to Athena using the CLI and  API via SDK and JDBC/ODBC. 
 
Athena integrates with Amazon QuickSight to create visualizations based on the Athena queries. 

Athena natively supports querying datasets and data sources that are registered with the AWS Glue Data Catalog.

### Pricing
- $5.00 per TB of data scanned (region dependent)
- Save from 30% to 90% on per-query costs by compressing, partitioning and using columnar format data(Parquet, AVRO)
- Charged for no of bytes scanned (minimum 10MB per query)
- Additional cost of source data stored in S3
- Additional Glue Data Catelog if used
- Bu default query result stored in S3. That charged seperately at standard S3 rates.
- Successful and canceled queries counted, failed query do not.

### Security
- Access control
    - IAM, ACLs and S3 bucket policies
    - Encryption at rest (SSE-S3, SSE-KMS and CSE-KMS)
    - Cross account access possible (using S3 Bucket policy)
    - TLS in-transit encrypts (between S3 and Athena)


### Misc.
- Add new data in existing table (ALTER TABLE ADD PARTITION) for partitioned table. There is no need to do anything if table is not partitioned.
- Support Quicksight and external BI tools using JDBC/ODBC.
- Athena support UDF.
Athena Support federated Query (run SQL queries across data stored in relational, non-relational, object, and custom data sources).
- Athena’s UNLOAD function to query the data and store the results in a specific file format on Amazon S3.

### Blog

### Docs
[AWS Athena FAQs](https://aws.amazon.com/athena/faqs/)

[AWS Athena User Guide](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)

### Code

