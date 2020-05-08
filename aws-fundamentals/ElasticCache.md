# Amazon ElasticCache 

## What is ElasticCache?

*Amazon Definition* <br>
Amazon ElastiCache allows you to seamlessly set up, run, and scale popular open-Source compatible in-memory data stores in the cloud. Build data-intensive apps or boost the performance of your existing databases by retrieving data from high throughput and low latency in-memory data stores.

*Breakdown* <br>
Amazon ElastiCache is a web service that makes it easy to deploy, operate, and scale an
in-memory cache in the AWS Cloud. The service improves the performance of web applications
by allowing you to retrieve information from fast, managed, in-memory caches
instead of relying entirely on slower disk-based databases.

## What is Cache?
In computing, the data in a cache is generally stored in fast-access hardware, such as
random-access memory (RAM), and may also be used in correlation with a software component.
A cache’s primary purpose is to increase data retrieval performance by reducing the
need to access the underlying slower storage layer.
Trading off capacity for speed, a cache typically stores a subset of data transiently, in
contrast to databases whose data is usually complete and durable.

#### Benefits
* Caches are in-memory databases with really high performance, low latency
* Helps reduce load off of databases for read intensive workloads
* Helps make your application stateless
* Improve application performance
* Reduce database cost
* Reduce load on the backend database tier
* Facilitate predictable performance
* Eliminate database hotspots
* Increase read throughput (IOPS)
The following types of information or applications can often benefit from caching:
* Results of database queries
* Results of intensive calculations
* Compute-intensive workloads that manipulate large datasets, such as highperformance
computing simulations and recommendation engines
Consider caching your data if the following conditions apply:
* It is slow or expensive to acquire when compared to cache retrieval.
* It is accessed with sufficient frequency.
* Your data or information for your application is relatively static
* Your data or information for your application is rapidly changing and staleness is not
significant.

## Caching Strategies
Two primary methods
are lazy loading and write through. A cache hit occurs when the cache contains the information
requested. A cache miss occurs when the cache does not contain the information
requested.

#### Lazy loading
Lazy loading is a caching strategy that loads data into the cache only when
necessary. When your application requests data, it first makes the request to the cache. If
the data exists in the cache (a cache hit), it is retrieved; but if it does not or has expired (a
cache miss), then the data is retrieved from your data store and then stored in the cache.
The advantage of lazy loading is that only the requested data is cached. The disadvantage is
that there is a cache miss penalty resulting in three trips:
1. The application requests data from the cache.
2. If there is a cache miss, you must query the database.
3. After data retrieval, the cache is updated.

#### Write through
The write-through strategy adds data or updates in the cache whenever
data is written to the database. The advantage of write through is that the data in the cache
is never stale. The disadvantage is that there is a write penalty because every write involves
two trips: a write to the cache and a write to the database. Another disadvantage is that
because most data is never read in many applications, the data or information that is stored
in the cluster is never used. This storage incurs a cost for space and overhead due to the
duplicate data. In addition, if your data is updated frequently, the cache may be updating
often, causing cache churn.

## In-Memory Key-Value Store
An in-memory key-value store is a NoSQL database optimized for read-heavy application
workloads (such as social networking, gaming, media sharing, and Q&A portals) or computeintensive
workloads (such as a recommendation engine). In-memory caching improves
application performance by storing critical pieces of data in memory for low-latency access.
Cached information may include the results of I/O-intensive database queries or the results
of computationally intensive calculations.

#### Benefits of In-Memory Data Stores
The strict performance requirements imposed by real-time applications mandate more
efficient databases. Traditional databases rely on disk-based storage. A single user action
may consist of multiple database calls. As they accumulate, latency increases. However,
by accessing data in memory, in-memory data stores provide higher throughput and lower
latency. In fact, in-memory data stores can be one to two orders of magnitude faster than
disk-based databases. <br><br>
As a NoSQL data store, an in-memory data store does not share the architectural
limitations found in traditional relational databases. NoSQL data stores are built to
be scalable. Traditional relational databases use a rigid table-based architecture. Some
NoSQL data stores use a key-value store and therefore don’t enforce a structure on the
data. This enables scalability and makes it easier to grow, partition, or shard data as data
stores grow. When consumed as a cloud-based service, an in-memory data store also provides
availability and cost benefits.

#### Benefits of Distributed Cache
A caching layer helps further drive throughput for read-heavy applications. A caching
layer is a high-speed storage layer that stores a subset of data. When a read request is sent,
the caching layer checks to determine whether it has the answer. If it doesn’t, the request
is sent on to the database.

The caching layer saves you money because you’re paying for one node instead of multiple
database nodes, and you get the added benefit of dramatically faster performance
for reads.

## ElastiCache
ElastiCache currently supports two different open-source, in-memory, key-value caching
engines: Redis and Memcached. Each engine provides some advantages.

#### Redis
Redis is an increasingly popular open-source, key-value store that supports more advanced
data structures, such as sorted sets, hashes, and lists. Unlike Memcached, Redis has disk
persistence built in, meaning that you can use it for long-lived data. Redis also supports
replication, which can be used to achieve Multi-AZ redundancy, similar to Amazon RDS.

**Key Points**
* in-memory key-value store
* Super low latency
* Has persistence for reboots
* Great to host
    * User sessions
    * Leaderboard (for gaming)
    * Distributed states
    * Relieve pressure on databases (such as RDS)
    * Pub / Sub capability for messaging
* Multi AZ with Automatic Failover for disaster recovery if you don’t want to
lose your cache data

#### Memcached
Memcached is a widely adopted in-memory key store. It is historically the gold standard
of web caching. ElastiCache is protocol-compliant with Memcached, and it is designed
to work with popular tools that you use today with existing Memcached environments.
Memcached is also multithreaded, meaning that it makes good use of larger Amazon EC2
instance sizes with multiple cores.

**Key Points**
* in-memory object store
* Cache doesn’t survive reboots
* Use cases:
    * Quick retrieval of objects from memory
    * Cache often accessed objects
* Overall, Redis has largely grown in popularity and has better feature sets
than Memcached.


## ElastiCache Solution Architecture - DB Cache
* Applications queries
ElastiCache, if not
available, get from RDS
and store in ElastiCache.
* Helps relieve load in RDS
* Cache must have an
invalidation strategy to
make sure only the most
current data is used in
there.

## ElastiCache Solution Architecture - User Session Store
* User logs into any of the
application
* The application writes
the session data into
ElastiCache
* The user hits another
instance of our
application
* The instance retrieves the
data and the user is
already logged in
