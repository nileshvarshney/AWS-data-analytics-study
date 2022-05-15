# ElasticCache
Amazon ElastiCache is a fully managed, in-memory caching service supporting flexible, real-time use cases. You can use ElastiCache for caching, which accelerates application and database performance, or as a primary data store for use cases that don't require durability like session stores, gaming leaderboards, streaming, and analytics. ElastiCache is compatible with Redis and Memcached. 

- Amazon ElastiCache improves the performance of web applications by allowing retrieve information from a fast, managed, in-memory system
- Reduce the cost associated with scaling web applications.
- AWS CloudFormation simplifies provisioning and management 
- Amazon ElastiCache offers fully managed Redis and Memcached
- Write Scaling using Sharding
- Read scaling using read replicas
- Multi AZ With Failover
- Fully managed

## Redis
- Redis is in-memory key-value store
- Super low latency ( sub ms)
- Cache Survive reboot by default
- Great to host:
    - User Session
    - Leaderboard (Game)
    - Pub/Sub capability for messaging
- Multi AZ, automatic failover
- Read replicas available during a primary node failure
- Support Read Replicas
- Inside VPC
- Read replica into a “standalone” primary node - not supported
- Provide service managed encryption at rest, but also have capability to use customer managed KMS

## Memcache
- Cache does not survive reboot
- Redis have better feature and more popular than memcache
