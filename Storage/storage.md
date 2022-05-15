# Storage and Data management
- Determine the operational characteristics of the storage solution for analytics
- Determine data access and retrieval patterns
- Select appropriate data layout, schema, structure, and format
- Define data lifecycle based on usage patterns and business requirements
- Determine the appropriate system for cataloging data and managing metadata

When you evaluate a storage solution, consider the different characteristics you require, such as cost, performance, durability, latency, consistency, and freshness of data. After you determine your requirements, you’ll be able to match them to the AWS service that best fits your needs.

AWS data stores are typically broken up into two main categories: operational and analytics.

### OPERATIONAL DATA STORES
Operational data stores (often referred to as OLTP data stores) consist mostly of transactional data and are built for quick updates. These storage systems are designed for high volume, low latency access, and are often regular, repeatable workloads.

Compared to analytic data stores, operational data stores are usually:
- Data stored in a row-based format
- Smaller compute size
- Low latency 
- High throughput
- High concurrency
- High change velocity
- Usually a good fit for caching
- Mission-critical, HA, DR, data protection
- (Amazon RDS, DynamoDB, ElasticCache, Amazon Neptune)

### ANALYTIC DATA STORES
Analytic data stores consist of two different types of data stores: OLAP and Decision Support Systems (DSS). OLAP systems provide a more responsive framework for real-time feedback and ad-hoc queries. DSS systems, such as data lakes and data warehouses, are useful for long-running query aggregations and projections, where latency is less important. 
 
Compared to operational data stores, analytic data stores are usually:
- Data commonly stored in a columnar format 
- Datasets are large and use partitioning
- Large compute size 
- Regularly performs complex joins and aggregations
- Bulk loading or trickle inserts
- Low change velocity
- Redshift and S3


