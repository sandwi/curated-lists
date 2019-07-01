# Redis

1. Redis should be used in cases where the optimal caching solution is key-value pairs.
2. There is a need to store data structure, beyond just key-value pairs.
2. The cache does not need to be extraordinarily large (less than a terabyte) or can fit in machine memory.
3. Replication is optimal vs. sharding. This is an appropriate choice for pure caching use cases, with relatively few writes and where the unavailability of cached data does not negatively impact the availability of the overall application (i.e. the data can be read from another system).
4. Speed and simplicity are the paramount.

### Apache Geode / Gemfire / Pivotal Cloud Cache (PCC)

Gemfire is an In-Memory-Data-Grid (IMDG) and a distributed hashmap. It is also a data store. it has a large feature set including strong consistency within a cluster, support for multiple data centers, reliable event delivery, and a strong security model. 

1. The cached data is extremely large (multi-terabyte) and requires sharding for horizontal scaling.
2. Geode/Gemfire is appropriate when there is need for high volume transaction systems with a lot of update contention. Gemfire supports scalable data consistency.
3. Geode/Gemfire is optimal when complex queries must be performed on the cached data.
4. Geode/Gemfire has an extensible security model, so custom security options may be easier to implement.
5. Geode/Gemfire can be used as a Compute Grid: when processing must be done close to the data because it is infeasible to move the data out of the store into a processing node.  
6. Cross-Data center two-way syncrhonous replication is required as Geode/Gemfire clusters can be replicated over WAN in various topologies: active-active, active-passive, ring, hub-spoke, star etc.

## References

- [Redis](https://redis.io/)
- [In-Memory Data Grid Explained](https://www.gridgain.com/resources/blog/in-memory-data-grid-explained)
- [In-Memory Data Grid vs In-Memory Databases](https://www.infoworld.com/article/3300747/in-memory-data-grids-vs-in-memory-databases.html)
- [Apache Geode](https://geode.apache.org/)
- [Gemfire](https://pivotal.io/pivotal-gemfire)
- [When to use Redis and When to use PCC](https://content.pivotal.io/blog/cache-rules-everything-around-me-when-to-use-redis-and-when-to-use-pivotal-cloud-cache)
- [Gemfire vs. Redis Comparison](http://vschart.com/compare/gemfire/vs/redis-database)
