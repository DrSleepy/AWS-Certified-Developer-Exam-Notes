# Elasticache

ElastiCache is similar to DAX.

Elasticache is a service that makes it easy to use an in-memory cache in the cloud.
It is a great way to cache frequently accessed data from a database so users can access it faster from the cache,
thus reducing the load on the database. Especially used on read-heavy databases.

**Good for:**

- faster reads
- read-heavy databases
- recommendation engines
- frequently accessed data
- output of compute intensive calculation

## Elasticache - Supported Cache Engines

1. Memcached -
   1. Object caching system
   2. Used when you are not concerned about redundancy (since no Multi-AZ capability, means no backups)
   3. Used primarily to ease the load on the database
   4. Good for multi-threaded applications
2. Redis -
   1. Open-source
   2. Key-Value caching system
   3. Supports Master / Slave replication
   4. Supports Multi-AZ access
   5. Supports failover, meaning it is replicated in case the primary case fails
   6. Used especially when working with leaderboards, sets and lists

### Lazy Loading

- Loads the data into the cache only when necessary
- If the requested data is in the cache, ElastiCache returns the data to the application
- If the data is not in the cache or has expired, ElastiCache returns null
- The application will then fetch the data from the database and writes the data recieved into ElastiCache for next time

**Advantages**

- Only requested data is cached
- Avoids filling up cache with useless data
- Node failures are not fatal as a new empty node will just have a lot of cache misses initially
- If an ElastiCache server fails, the request will just go to DynamoDB whilst a new ElastiCache server is being started

**Disadvantages**

- If an ElastiCache server is down, you still have to pay for the extra call to ElasticCache before actually retrieving the data from DynamoDB
- Data is ONLY updated when there is a cache-miss, so data can become stale
  - mitigated by setting a TTL on the record

### Write-Through

- Adds or updates data to the cache whenever data is written to the database

**Advantages**

- Data in the cache is never stale
- Users are generally more tolerant of additional latency when updating data than when retrieving it

**Disadvantages**

- Wasted resources if most of the data is never read
- An extra call is ALWAYS made to update the cache (expensive)
- If a node fails and a new one is spun up, data is missing until added or updated in the database
  - mitigated by implementing Lazy Lodading in conjunction with Write-Through

### DAX vs ElastiCache

- DAX was specifically made for DynamoDB
- DAX only supports Write-Through
- ElastiCache is usually used for RDS
