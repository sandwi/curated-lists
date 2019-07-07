**Table of Contents**
1. **Distributed Systems Bulding Blocks**
   1. [Consensus Protocols](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/README.md#consensus-protocols)
   1. [Service Registry](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/README.md#service-registry)
   1. [Consistent Hashing](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/README.md#consistent-hashing)
1. [Resource Schedulers](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/README.md#resource-schedulers-aka-containerized-workload-managers)
   
   
# Distributed Systems Building Blocks
## Consensus Protocols
* Paxos
  * [Paxos Paper](https://www.microsoft.com/en-us/research/uploads/prod/2016/12/The-Part-Time-Parliament.pdf)
  * [Paxos Simplified](https://www.microsoft.com/en-us/research/uploads/prod/2016/12/paxos-simple-Copy.pdf)
* Raft
  * [Raft](https://raft.github.io/)
  * [Talk on Raft by John Ousterhout](https://raft.github.io/slides/uiuc2016.pdf)
* [ZooKeeper Atomic Broadcast (ZAB)](https://cwiki.apache.org/confluence/display/ZOOKEEPER/Zab1.0)

## Service Registry
* [Hashicorp Consul](https://www.consul.io/)
* [CoreOS etcd](https://etcd.io/)
* [ZooKeeper](https://zookeeper.apache.org/)
* [Netflix Eureka](https://github.com/Netflix/eureka/wiki)
  
## Consistent Hashing
* Original Paper that described Consistent Hashing (theoretical paper) by David Karger et. al., [Consistent Hashing and Random Trees: Distributed Caching Protocols for Relieving Hot Spots on the World Wide Web](https://www.cs.princeton.edu/courses/archive/fall09/cos518/papers/chash.pdf)
* Paper from original authors describing an implementation for web caches using consistent hashing by David Karger et.al., [Web Caching with Consistent Hashing](https://web.archive.org/web/20120504040223/http://www8.org/w8-papers/2a-webserver/caching/paper2.html)
* Wikipedia entry on [Consistent Hashing](https://en.wikipedia.org/wiki/Consistent_hashing)
* [Michael Nielsen's Blog on Consistent Hashing](http://michaelnielsen.org/blog/consistent-hashing/)
* [Good Read on Consistent Hashing](https://www.ably.io/blog/implementing-efficient-consistent-hashing)
* Implementations
  * [Tom White's Java Implementation](https://web.archive.org/web/20120605030524/http://weblogs.java.net/blog/tomwhite/archive/2007/11/consistent_hash.html)
  * [Cloudera's Java Implementation](https://github.com/cloudera/flume/blob/master/flume-core/src/main/java/com/cloudera/util/consistenthash/ConsistentHash.java)
 
 ## Bloom Filters
 Bloom filters are very useful data structures and are used by distributed databases like BitTable or Cassandra or relational databases like Oracle, Postgres etc to avoid  disk lookups for non-existent rows or columns.
 * Wikipedia Entry on [Bloom Filter](https://en.wikipedia.org/wiki/Bloom_filter)
 * [Bloom Filters by Example](https://llimllib.github.io/bloomfilter-tutorial/)
 * Google Guava's [Bloom Filter](https://github.com/google/guava/wiki/HashingExplained#bloomfilter)

# Resource Schedulers (aka Containerized Workload Managers)
* [Kubernetes](https://kubernetes.io/)
  * [Google Made Its Secret Blueprint Public to Boost Its Cloud](https://www.wired.com/2015/06/google-kubernetes-says-future-cloud-computing/)
* Google Borg
  * [Large-scale cluster management at Google with Borg](https://ai.google/research/pubs/pub43438)
  * [Borg: The Predeccesor to Kubernetes](https://kubernetes.io/blog/2015/04/borg-predecessor-to-kubernetes/)
  * [What Google Learned From the Borg About Container Management](https://thenewstack.io/google-learned-borg-container-management/)
  * [You Want To Build an Empire Like Google's? This is Your OS](https://www.wired.com/2016/04/want-build-empire-like-googles-os/)
  * [Return of the Borg: How Twitter Rebuilt Google's Secret Weapon](https://www.wired.com/2013/03/google-borg-twitter-mesos/)
* Google Omega
  * [Omega: flexible, scalable schedulers for large compute clusters](https://ai.google/research/pubs/pub41684)
  * [Borg, Omega, and Kubernetes](https://queue.acm.org/detail.cfm?id=2898444)
* [Mesos](http://mesos.apache.org/)
* [Cloud Foundry Diego](https://docs.cloudfoundry.org/concepts/diego/diego-architecture.html)

