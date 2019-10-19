## Accellorator (DAX)

DAX is similar to ElastiCache.

- Dax is an in-memory cache (like ElastiCache, which uses Redis) for DynamoDB
- Improves read performance by up to 10x
- Microsecond performance for millions of requests per second
- Ideal for read-heavy and bursty workloads
- Dax is a write-through caching service -
  - which means data is written to the cache as well as DynamoDB at the same time
- DynamoDB API calls are first sent to the cache (cache hit) -
  - if result not found, it will then search DynamoDB which will perform an Eventual Consistent GetItem operation
- Can help reduce Provisioned Read Capacity on the DyanmoDB tables
- Can ONLY handle Eventually Consistent Reads
- Not suitable for write-heavy workloads
- Not suitable for applications that do not require microsend response times

### DAX vs ElastiCache

- DAX was specifically made for DynamoDB
- DAX only supports Write-Through
- ElastiCache is usually used for RDS
