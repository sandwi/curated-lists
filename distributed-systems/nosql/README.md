**Table of Contents**
1. [NoSQL Concepts](https://github.com/sandwi/curated-lists/tree/master/distributed-systems/nosql#nosql-concepts)
1. [Key-Value Databases](https://github.com/sandwi/curated-lists/tree/master/distributed-systems/nosql#key-value-databases)
1. [Document Databases](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/nosql/README.md#document-databases)
1. [Column-Family Databases](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/nosql/README.md#column-family-nosql-databases)
1. [Graph Databases](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/nosql/README.md#graph-databases)
1. [Time-Series Databases](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/nosql/README.md#time-series-databases)  
   
[DB-Engines](https://db-engines.com/en/) - For Comprehensive listing of various NoSQL Databases

# NoSQL Concepts
* Wikipedia Entry on [NoSQL](https://en.wikipedia.org/wiki/NoSQL)
* Martin Fowler's definition [NosqlDefinition](https://martinfowler.com/bliki/NosqlDefinition.html)
* [CAP Theorem](https://github.com/sandwi/curated-lists/blob/master/distributed-systems/distributed-databases/README.md#cap-theorem)
* Werner Vogel's [Eventually Consistent - Revisited](https://www.allthingsdistributed.com/2008/12/eventually_consistent.html)
* [BASE: An Alternative to ACID](https://queue.acm.org/detail.cfm?id=1394128)

# Key-Value Databases
* Simple Caches (In-Memory K-V Stores)
  * [Redis](https://redis.io/) - More of a data structure server, includes K-V
  * [Memcached](http://www.memcached.org/)
* In-Memory Data Grids (IMDGs)
  * [Apache Geode](https://geode.apache.org/) - Open Sourced Pivotal GemFire
    * [Pivotal GemFire](https://pivotal.io/pivotal-gemfire) - In-Memory Data Grid & Database with optional persistence
  * [Apache Ignite](https://ignite.apache.org/) - Multi-Model NoSQL database, formerly GridGain
  * [Oracle Coherence](https://www.oracle.com/middleware/technologies/coherence.html)
    * [Cohorence Website](http://coherence.java.net/)
    * [Coherence Incubator - Open Source patterns/libraries](https://github.com/coherence-community/coherence-incubator)
  * [Hazelcast](https://hazelcast.com/)
  
## Cloud K-V Databases
* **DynamoDB**
  * [DynamoDB Paper](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf)
  * [DynamoDB Documentation](https://docs.aws.amazon.com/dynamodb/index.html)
  * DynamoDB Modeling
    * [Best Practices for Modeling Relational Data in DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-relational-modeling.html)
    * [Example of Modeling Relational Data in DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-modeling-nosql-B.html)
    * [Adjacency List Design Pattern](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-adjacency-graphs.html#bp-adjacency-lists) - Pattern for modeling many-to-many relationships
    * [DynamoDB: Data Modeling](https://medium.com/hotels-com-technology/dynamodb-data-modeling-c4b02729ac08)
    * [From relational DB to single DynamoDB table: a step-by-step exploration](https://www.trek10.com/blog/dynamodb-single-table-relational-modeling/)
    * [Video - AWS Builders' Day | DynamoDB and Schema Design](https://www.youtube.com/watch?v=ziqm6q-JsGQ)
  * [DynamoDB Guide](https://www.dynamodbguide.com/the-dynamo-paper/)
  * DynamoDB Best Practices
    * [AWS's DynamoDB Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)
  * DynamoDB Challenges
    * [Why Amazon Dynamodb Isn't for Everyone and How to Decide When it's for You](https://read.acloud.guru/why-amazon-dynamodb-isnt-for-everyone-and-how-to-decide-when-it-s-for-you-aefc52ea9476)
* [Amazon SimpleDB](https://aws.amazon.com/simpledb/)
* [Microsoft Azure CosmoDB](https://azure.microsoft.com/en-us/services/cosmos-db/) - Globally distributed, horizontally scalable, multi-model database service

# Document Databases
* [MongoDB](https://www.mongodb.com/)
* [Apache CouchDB](http://couchdb.apache.org/)

## Cloud Document Databases
* [DynamoDB](https://docs.aws.amazon.com/dynamodb/index.html)
* [Microsoft Azure DocumentDB](https://azure.microsoft.com/en-us/resources/videos/introduction-to-azure-documentdb/)
* [Microsoft Azure CosmoDB](https://azure.microsoft.com/en-us/services/cosmos-db/) - Globally distributed, horizontally scalable, multi-model database service

# Column-Family NoSQL Databases
* Google BigTable
  * [Google BigTable Paper - Bigtable: A Distributed Storage System for Structured Data](https://research.google.com/archive/bigtable-osdi06.pdf)
* Apache Cassandra
  * [Apache Cassandra](http://cassandra.apache.org/)
  * Data Modeling
    * [Basic Rules of Cassandra Data Modeling](https://www.datastax.com/dev/blog/basic-rules-of-cassandra-data-modeling)
    * [EBay's Blog on Cassandra Data Modeling Best Practices Part 1](https://www.ebayinc.com/stories/blogs/tech/cassandra-data-modeling-best-practices-part-1/)
    * [Designing data models for Cassandra](https://www.oreilly.com/ideas/cassandra-data-modeling)
    * [Cassandra Data Modeling: Primary, Clustering, Partition, and Compound Keys](https://dzone.com/articles/cassandra-data-modeling-primary-clustering-partiti)
    * [Understand the Cassandra data model](https://pandaforme.gitbooks.io/introduction-to-cassandra/content/understand_the_cassandra_data_model.html)
* [Apache HBase](http://hbase.apache.org/)

## Cloud Column-Family Databases
* Google BigTable
  * [Google BigTable Cloud Service](https://cloud.google.com/bigtable/)
  * [Google BigTable Documentation](https://cloud.google.com/bigtable/docs/overview)
  * [BigTable: Designing Your Schema](https://cloud.google.com/bigtable/docs/schema-design)
* [Microsoft Azure CosmoDB](https://azure.microsoft.com/en-us/services/cosmos-db/) - Globally distributed, horizontally scalable, multi-model database service

# Graph Databases
* [Neo4j](https://neo4j.com/)
* [Graph Databases for Beginners](https://neo4j.com/blog/why-graph-databases-are-the-future/)
* [OrientDB](https://orientdb.com/graph-database/)
* [JanusGraph](https://janusgraph.org/) - Graph database backed by Google, IBM, a Linux Foundation project
  * [JanusGraph: A highly scalable graph database](https://opensource.google.com/projects/janusgraph)

## Cloud Graph Databases
* [Microsoft Azure CosmoDB](https://azure.microsoft.com/en-us/services/cosmos-db/) - Globally distributed, horizontally scalable, multi-model database service
* [Amazon Neptune- The Graph Databases Defined](https://aws.amazon.com/nosql/graph/)

# Time-Series Databases
* [InfluxDB](https://www.influxdata.com/products/influxdb-overview/)
* [TimescaleDB](www.timescale.com)
* [OpenTSDB](http://opentsdb.net/)
* [Apache Druid](https://druid.apache.org/) - Multi-Model DB, primarily time-series database



