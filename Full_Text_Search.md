# Full Text Search
You joined a new project. The project is going through some performance and scaling issues. After some analysis,  
the team lead asks you to investigate the possibility of using a different database for full text searching will improve performance.  
Investigate Elasticsearch, Solr, and Lucene.

## There are various possibilities of performance slow down
1. __Elastic Search__: is a great search engine that helps retrieve data in near-real time and also helps store data efficiently to do so.
   But as data grows and complexity increases, we start seeing performance slow down.
2. __Solr__:
3. __Lucene__: Lucene is a high-performance, full-featured text search engine library written in Java.   
   It is a technology suitable for nearly any application that requires full-text search, especially cross-platform.

__Performance fix__:
 - Elasticsearch needs a healthy amount of cache, disk space, RAM also needs a powerful CPU. So first up we will check for all these hardware
   issues. If there is anything which affects the performance we will either change it or increase its quantity. Also if the system is still  
   using a mechanical hardware drive, it should be replaced with SSDs.
 - In production, we have multiple nodes running. If we get a large number of requests we have to divide the load beetween nodes to decrease strain 
   on a particular node. To do this we use load balancing. Load balancing distributes the load to multiple nodes, which reduces the load on 
   each node, thus increasing performance. To enable load balancing is quite easy, we just need to configure node as coordinating only node, 
   which will enable smart load balancing.
 - 
