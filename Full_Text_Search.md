# Full Text Search
__Task__: The project is going through some performance and scaling issues. After some analysis, the team lead asks you to investigate 
   the possibility of using a different database for full text searching will improve performance.

## Technologies which might causes the performance issues
1. __Elastic Search__: Elastic search is a great search engine built on Lucene that helps retrieve data in near-real time and also helps store data efficiently to do so. But as data grows and complexity increases, we start seeing performance slow down.
2. __Solr__: Solr is the popular, blazing-fast, open source enterprise search platform built on Apache Lucene 
3. __Lucene__: Lucene is a high-performance, full-featured text search engine library written in Java.   
It is a technology suitable for nearly any application that requires full-text search, especially cross-platform.

__Performance fix__:
 - Firstly, check for update for all the software, as with every update companies brings various bug fixes and performance improvements.
 - Elasticsearch needs a healthy amount of cache, disk space, RAM also needs a powerful CPU. So first up we will check for all these hardware issues. If there is anything which affects the performance we will either change it or increase its quantity. Also if the system is still using a mechanical hardware drive, it should be replaced with SSDs.
 - In production, we have multiple nodes running. If we get a large number of requests we have to divide the load beetween nodes to decrease strain on a particular node. To do this we use load balancing. Load balancing distributes the load to multiple nodes, which reduces the load on each node, thus increasing performance. To enable load balancing is quite easy, we just need to configure node as coordinating only node, which will enable smart load balancing.
 - Increase the size of index buffer, if the buffer is getting full before  its document are written on disk.
 - If the request rate is high, scale up your install by adding additional copies of index and additional servers.
 - If the index is updating frequently, we can designate shards to spread the indexing load evenly across all nodes. We can add one, two or more shard per node depending on CPU and disk bandwidth on nodes.
 - Increase the refresh interval depending on indexing period.
 - The most common reason for slow startup is Solr's update log feature. It add transaction log for all updates. To fix this we need to keep our transaction log size down. The only way to do this is by sending frequent hard commits. Hard commit closes the current transaction log and starts a new one. Solr only keeps enough transaction logs around to be able to restore the last 100 documents that were indexed, but it cannot rip apart an individual log file, so if the newest log file is very very large, it must keep the whole thing and replay it at startup.
 - Check if Lucene is using enough threads to fully utilize the computer's hardware. Increase the thread count until throughput no longer improves, also keep latency in check.
 - Configure filter cache. filter cache allows to control over how filter queries are handeled in order to maximize performance.

If the performance is still sluggish even after performing these many checks then we should consider looking out for some other databases.


## References
1. ["How to solve 5 Elasticsearch performance and scaling problems"](https://www.datadoghq.com/blog/elasticsearch-performance-scaling-problems/) by Emily Chang - September 26,2016
2. ["7 Effective Ways to Improve Your Elasticsearch Performance"](https://www.scalyr.com/blog/improve-your-elasticsearch-performance/) by Erin Baez - March 9,2021
3. ["Solr Performance Problems"](https://cwiki.apache.org/confluence/display/solr/solrperformanceproblems) by Shawn Heisy - April 07,2021
