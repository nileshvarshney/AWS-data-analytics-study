# DMS - Data Migration Service
- Migrate databases to AWS quickly and securely
- The source database remains fully operational during the migration, minimizing downtime to applications
- Supports homogeneous migrations such as Oracle to Oracle
- Supports heterogeneous migrations such as Oracle or Microsoft SQL Server to Amazon Aurora.
- Replicate from multiple sources to S3 to build highly available and scalable lake solution
- Simple to Use and low cost
- You must create an EC2 instance to perform the replication tasks.

# SCT - Schema Conversion Tool
- Convert database schema from one engine to other including views, stored procedures and functions.

# Direct Connect
- Dedicated private connection between VPC and remote network
- Can setup multiple of 1Gbps or 10Gbps dedicated network
- To access the VPC you need to set up Virtual private gateway
- You can access the public S3 directly through Direct connect
- Single connection from remote can access both VPC(through virtual private gateway) and S3
- Support both IPv4 and IPv6
- For high Availability - (Two Direct Connect as failover OR Site-to-Site VPN as a failover)

![Direct connect](images/direct-connect-overview.png)


# Direct Connect Gateway
- To connect more than one VPC in many different region within same account

![Direct Connect Gateway](images/dx-gateway.png)

# Snowball
- Physical storage devices to transfer large amounts of data
- Protected by the AWS Key Management Service (AWS KMS).
- 80 TB and 50 TB models are available in US Regions.
- Snowball doesn't support international shipping or shipping between AWS Regions outside of the US.
- Tracking using SNS and text messages
- E Ink display – used to track shipping information and configure your IP address.
- Snowball Process
    - Request a snowball
    - install snowball client on your server
    - connect snowball to your server and copy data file
    - Ship back the device
    - Data will be loaded into S3
    - snowball will be completely wiped 

# Snowball Edge
- Snowball with computational capacity
- 100 TB capacity
    - Storage Optimized (24 vCPU)
    - Compute Optimized (52 vCPU & optional GPU)
- Support custom Lambda function
- Pre-process the data while moving
- IoT Greangras ( Not available in Snowball)
- 100 TB (80 TB usable)
- 100 TB Clustered (45 TB per node)
- LCD display – used to manage connections and provide some administrative functions.
- E Ink display – used to track shipping information and configure your IP address.

# Snowmobile
- Transfer exabytes of data
- Each Snowmobile has 100PB of capacity
- Better than Snowball if you transferring more than 10PB of data.
