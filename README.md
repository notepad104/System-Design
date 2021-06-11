System Design
* Clarify Requirements
  * Features
  * Non Functional Requirements

* Sketch Out HLD

* Back of the enveloper calculation
 * 1 Billion per month = 400 per second
 * 1 Billion per day = 10000 per second
 * 2.5 million seconds per month
 * 1 request per second = 2.5 million requests per month
 * 40 requests per second = 100 million requests per month
 * 400 requests per second = 1 billion requests per month

* Discuss individual components and how they interact in detail
  * Reverse Proxy (Eg. Varnish)
  	* Centralized internal services
  	* Sits in front of web servers and is face of client calls
  	* Provides dditional security, caching, intelligent routing etc.

  * App Servers
  	* Service Discovery
  	  * How do services find each other ?
  	  * Zoopkeeper can be used to register each service and query
  	  * Service to Service Communication / Authorization
  	* MicroServices
  * Data Tier
  	* If Read heavy or write heavy 
  	* Read heavy -- cache
  	* User profile -- SQL
  	* Feeds -- HBase / Cassandra
  * Back of the envelope calc
  	* Users : 10 ^ 10
  	* Requests per day
  	* Reads/Writes

 * Communication
 	* How different components interact with each other ?
 	* TCP -- reliable and connetion based (HTTP)
 	* RPC --  Remote invocation over the network, simple, smaller payloads and faster, rich DS (map, list)
 		* Stub Procedure -- Marshalls arguments into request message and unmarshals response
 		* Communication Module -- Communicate remotely with server communication module

 * Storage
   * Relational
   	* ACID -- Atomicity, Consistency, Isolation, Durability
   	* Schema Design & 3NF -- To reduce redundancy and improve consistency, people follow 3NF 
   		* 1NF -- tabular, each row-column contains only 1 val
   		* 2NF -- primary key determines all the attributess
   		* 3NF -- candidate keys determine all the attributes
    * reading from a disk, relational join operation is time consuming and 99% of the time is spent on disk seek
   	* distributed join operation across networks.
   	* denormalization is introduced by adding redundant data or by grouping data.

   	* DB Proxy
   		* Eliminate Single Point of failure
   		* DBProxy to ditribute data
   			* Clustering -- Decentralized solution, everything is automatic, data is distributed, moved and automatically rebalanced
   			* Shariding -- centralized solution, Data is distributed manually and does not move. Nodes are not aware of each other.

   * NoSQL
   	 * Read write ratio, 1000:1
   	 * Key-Value Store (Cache):
   		* giant hashtable/hashmap/dictionary
   		* redudce latency, O(1) read write on faster memory
   		* Pattern : Read Through ? Write Through ? Write Around ? Write Back ? Cache Aside ?
   		* Placement : Where to place ? client side / server side ?
   		* Replacement : TTL ? Invalidate ? LRU ?
   		* Choices
   			* Redis -- data persistence
   			* Memcached -- no data persistence

    * Document Store:
    	* Abstracted like KV store, Documents like XML, JSON in value
    	* provides flexibility -- schemaless document
    	* performance -- by breaking 3NF
    	* MongoDB, CouchDB
    
    * Column Store:
    	* Abstraction like Giant nested map, ColumnFamily<RowKey, Columns<Name, Value, Timestamp>>
    	* distributed, highly available, optimized for writes
    	* Cassandra, HBase, DynamoDB
    
    * Graph DB:
    	* Abstraction is graph
    	* stores entities and relationships b/w them
    	





