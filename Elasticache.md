# Elasticache

Elasticache is a web service that makes it easy to use an in-memory cache in the cloud.
It is a great way to cache frequently access data from a database so users can access it faster from the cache,
thus reducing the load on the database. Especially used on read-heavy databases.

## Elasticache - Supported Cache Engines

1. Memcached -
   1.1 Object caching system
   1.2 Used when you are not concerned about redundancy
   1.3 Used primarily to ease the load on the database
2. Redis -
   2.1 Key-Value caching system
   2.2 Supports Master / Slave replication
   2.2 Supports Multi-AZ access
   2.3 Supports failover, meaning it is replicated in case the primary case fails
   2.4 Used especially when working with leaderboards, sets and lists
