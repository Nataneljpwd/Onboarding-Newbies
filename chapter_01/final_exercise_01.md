# Final Exercise 01 - Introduction to Hadoop Ecosystem - Q&A :question:

## Goals:
- Gain a foundational understanding of the Hadoop ecosystem.
- Explore key components and their roles in big data processing.
- Make connections between the Hadoop ecosystem and real-world use cases.
- Develop a high-level understanding of the Hadoop ecosystem and its role in big data processing.
- Familirize yourself with the Hadoop ecosystem and its role in big data processing.
- Start to work with time estimation and planning.
- Learn to ask questions and how to find the answers with deep understanding of the whole concept.
:warning: **Note:**
- Maybe this is the first time you need to answer questions with your own words, so take your time to read the instructions carefully and ask your mentor if you have any questions.
- Take time to think about the answers, don't just copy-paste from the internet.
- Try to differ between the important and less important information.

## Chapter 12: Q&A and Discussion
- Open forum for questions, clarifications, and discussions with the mentor.
- Reflection on the day's learnings and exploration of potential project applications.

### Chapter 1: Introduction to Big Data and Hadoop

## Additional questions:

- [x] *Hdfs Architecture*:
  - [ ] *Hdfs 1.x*: In hadoop version 1, there was only one Namenode and it was the sigle source of failure of the system.
  - [ ] *Hdfs 2.x*: Hadoop version 2 introduced which included a standby Namenode which in case of failure of the main name node, it replaces it, thus, removing the single source of failure, however, the name node recovery has to be done manually.
  - [ ] *Hdfs 3.x*: Introduced support for multiple active namenodes which allow for High availability and now, namenode recovery is done automatically.

- [x] *Hdfs VS S3*: 
  - [ ] *Hdfs*: A distributed file system that allows for storage of files in a hirarchiel FS, and allows for data querying and processing using tools such as MapReduce and Spark, in addition to the ability to utilize the GPU (as of hadoop 3.x) along with spark, however hdfs is usually self managed or managed using external vendors which come with a not so small cost, while the availability of these systems is lower than the availability of S3 which is managed by amazon and and is cheaper.
        Hdfs also allows for querying on the data using apache Impala, Hive and Hbase 
  - [ ] *S3* (Simple Storage Service): can only store and retrieved objects by their key / name, no querying can be done on the s3 and it is not a file system, meaning there are no folders, only file names, S3 allows to tag and store some additional metadata along with the file, has a very simple REST api that can be used and is managed by amazon, with other S3 compatible systems such as Minio that are also Object storage.
        S3 is relatively cheap, as you only pay for what you use, in addition to it being managed by Amazon which have the resources and the knowledge to provide extremely high availability (11 nines!) with good performance and a good cost.

- [x] *Hdfs use cases*: to store large amounts of files that need to be searchable (Websites and text / pdf files), hadoop is often used in the finance industry for risk modelling (using big data that is stored in hdfs and analyzing with mapreduce and spark), can also be used like a regular file / block storage that can handle a lot of data and scale easily while being reliable, Hdfs can also be used along with analytics tools to detect fradulent activity.

- [x] *Terms*:
  - [x] *Failover*: The process of handling a node / master failure, when a leader fails, a failover event is triggered and a leader re election starts.
  - [x] *Fencing*: Isolation of a node or shared resources when a node seems to be malfunctioning.
  - [x] *Zkfc*:  The Zookeeper Failover Controller which is responsible for automatic failover in distributed systems like Hadoop (namenode failover) and Kafka (Controller failover)
  - [x] *Quorum*: Quorum (in zookeeper) is the smallest amount of running servers of a distributed system in order for it to work and be available for the clients, usually the formula for a quorum is that if you have 2n + 1 nodes, n nodes can fail and the system will keep working as it worked before.
  The quorum can also be used to elect leaders, by having a quorum of the in sync nodes that can become leaders in the case of node failure.


1. **Q:** What is Apache Hadoop?
1. **A:** Hadoop is a distributed file system that works based on a master-slave architecture which was built with the assumption that hardware failure is the norm.
Hadoop is unique in comparison to other DFS because hadoop was built to scale from multiple compters to a few thousands of computers easily while utilizing the computational power and the storage of all the computers, in addition, hadoop processes and stores the data in the same place rather than moving the data to a different place to be processed.
Hadoop also contains YARN which allows for better and more efficient resource utilization in addition to allowing multiple processes to run in parrallel.
Hadoop is a rack aware system which means that hadoop knows the physical network topology (through a resolve api call through rpc) and can place the data in those placed accordingly to ensure maximum fault tolorence evenif one rack goes down
Before hadoop, storage and processing of large quantaties of data was very hard and required a lot of expensive hardware and cost a lot to run.
after hadoop came, it allowed to store large quantaties of data and to scale to an unlimited number of nodes which was not possible before.

Hadoop started in 2006 by Doug Cutting (working at yahoo at the time) after he and Mike Cafarella had worked on the apache Nutch project which was supposed to be a search engine which could index 1 billion pages but after Doug realized that it could only scale to 20-40 nodes and that it would be too expensive to run, so Doug decided to create a new project named hadoop (the name of his son's yellow elephant toy) and in 2007, yahoo was able to scale hadoop to 1000 nodes and use it,
in 2008, yahoo has open sourced the project and in july they were able to scale it to 4000 nodes.
In 2009, Doug left Yahoo and went to work at cloudera, in 2011 Apache released Apache hadoop version 1.0 and in 2013 Hadoop 2.0.6 was available and in 2017 version 3.0 came out.
The main problems with hadoop are that hadoop is very bad with small files because of the way it stores data, for each block, the namenode stores metadata about the files (the locations of them in datanodes and the file system structure).
now, instead of managing a small number of computers, we need to manage all the nodes either ourselves or through a vendor providing us managed hadoop cluster.



2. **Q:** Can you name a few vendor-specific distributions of Hadoop?
2. **A:** *Cloudera Distribution Platform* - A managed distribution by cluodera which includes a cloudera cluster manager, integrated security and data governance, *Amazon Elastic MapReduce* - A managed distribution of hadoop with a pay-per-use billing system, automatic scaling and easy integration with other aws products, *Microsoft azure HDInsight* - includes integration with microsoft tools like Power BI and Azure data factory, also billed as a pay-per-use patform.



3. **Q:** What are the three modes in which Hadoop can run?
3. **A:** **Standalone (default)** - where it runs as a single java process, used to debug and make simple POC's just to test on a local machine with a small amount of data and is easy and quick to setup, mostly used for quick tests, **Psuedo Distributed** - where there is a single node cluster (many processes on one machine) which simulates the real world but still runs on one machine which is used to test and debug more like a staging area but is more resource intensive and takes more time to setup, **distributed** - a multi node cluster which includes the Namenode, Secondary Namenode and the Datanodes, this is used ion the real world where we need to actually process and store very large amounts of data quickly and efficiently, it is what we use to make big data queries and get valuable knowledge from them.



4. **Q:** What is the primary role of the `hadoop-env.sh` configuration file?
4. **A:** The primary role of the hadoop-env is to set environment variables for hadoop and customize the options of the hadoop processes, like client ops (port and host of the cluster), the size of the Mapreduce heap, the classpath of the hadoop scripts and more, in addition to setting up various jave related options like the Hadoop classname which sets the java class against which the hadoop specific variables that it will run against when the excecution of a process continues

5. **Q:** What purpose does the `core-site.xml` file serve?
5. **A:** The purpose of the core site is to configure mostly IO related things and also the filesystem and network addresses.
some examples include: 
 - [x] hadoop.security.authentication - either simple (no auth) or kerberos, sets whether to use authentication and which type
 - [x] hadoop.tmp.dir - the base directory where hadoop can store temporary files
 - [x] hadoop.security.dns.nameserver - the hostname / ip addr of the dns server which the kerberos service nodes use to their own hostname for kerberos login
 - [x] io.bytes.per.checksum - the number of bytes to use per checksum, must be less then io.file.buffer.size
 - [x] io.file.buffer.size - sets the buffer size for seqeunce files during read and write opperations (sequence files are binary files containing key-value paris which were created to solve some of the small file problems in hadoop by having multiple files inside one block file)

### Chapter 2: Hadoop Distributed File System (HDFS)

6. **Q:** What is HDFS?
6. **A:** HDFS is the Hadoop distributed system which is basically like a regular file system but it is distributed between multiple computers.
HDFS is built for fault tolorence meaning, it was built with the idea that hardware failures are a norm and happen a lot so hdfs uses replication and redundency to keep the system highly available and fault tolorent.
HDFS is the primary storage of the Hadoop applications, based on java and which contains data nodes and name nodes, the *name nodes* are the nodes which monitors all the data stored, replica counts and the amount of data nodes which are alive and the FS structure.
the *data node* is the node that stores the data itself in the form of blocks which have a max size of a preconfigured amount, default is usually 128 MB but sometimes can be 64 or 256 MB by default.
It is a rack aware system which means that it knows the physical topology of the network and the connected nodes which it uses to enhence fault tolorence by splitting replicas to different racks (an example with 3 replicas and 2 racks, hadoop will store one replica on the same rack with the name node and 2 more replicas on different racks in a different location / switch).

provides High availability using 2 Name nodes with one being active and one being a standby, in case the active node will fail.

Hdfs also has journal nodes which store changes to the file system (file addition, deletion and more) which is an edit log which is used to build the FSImage and the file system structure in the ram.

Hdfs knows that "moving data is more expensive than moving computation" so it has minimal data movement and makes most of the computations in the same node that stores it's data.

7. **Q:** What is the role of the NameNode in HDFS?
7. **A:** The role of the NameNode is to save metadata about the file and to manage where they are saved, in addition to managing and saving the FS structure and also replicate / delete replications as needed.
the metadata is stored in memory and also in a persistant FSImage file, in addition to a local editlog which includes the logs of all the eddits that have happened to the file system structure.
the namenodes also monitors all the data nodes and knows which are alive and which are down.

8. **Q:** What is a DataNode in HDFS?
8. **A:** A DataNode is the node that saves the data itself in the form of blocks with a max size that was configured beforehand in the hdfs-site.
The datanode also performs the computations and analysis of the data on the machines which allows for less movement of data.
the data nodes send a block report every 6 hours to the namenode which includes all the blocks stored in this data node, in addition to the name of the file, the path ("virtual path") and the block count.
the data node stores metadata about the file as well, with the same name of the file (blk_{GeneratedNumber}) with the suffix ".meta" which includes the file name, the file path, the block count, the block id, permissions of the file, owner, updated at and other time metadata and file size.

9. **Q:** How does HDFS achieve fault tolerance?
9. **A:** Hdfs achieves fault tolorence by using *redundency and replication* - duplicating the data multiple times and storing it on different machines so that if hardware failure were to occur, other machines store the replicas so they can be read from there, *rack awareness* - hdfs knows the physical network topology of the datanodes and namenodes and it uses it to better spread the replicas so that even if a rack falls or a network failure occurs, there will still be available replicas on a different switch/rack (if 3 replicas are set, one replica will be stored in the same place as the namenode and the 2 others will be stored in a different rack), in addition to *journal nodes* - nodes that store edit logs of the file system which can be used to reconstruct the file system structure in case of namenode failure and *secondary namenode* - a namenode that takes the edit logs file from the main namenode and constructs the fs image using the current fsimage and updates it in the main namenode, the reason for this is that usually the fs image only gets updated when the namenode restarts which can take a while which will cause the name node to fail the readiness check or crash, so the secondary namenode was created to mitigate this issue by periodically reconstructing the fs image and clearing the edit logs and *Standby namenode* - which waits and periodically syncs with the main name node and is there in case the main namenode crashes, the secondary namenode starts getting the requests and monitoring the dœ†a nodes.

10. **Q:** Can you explain rack awareness in HDFS?
10. **A:** Rack awareness means that hadoop knows the physical network topology of the network, which allows hadoop to distribute the files such that even if a rack crashed, the data is still available.
the rack awareness is done by the name node and the job manager which send an rpc resolve request to to all the nodes and use it to get the rack and the host of the node when it starts.
the practical use of the rack awareness comes when deciding where the replications go, in the case of 3 replications, one replica will be stored in the same rack as the name node and the other 2 will be stored on a different rack, in order to have the least amount of traffic between racks and to allow for fault tolorence in the case a rack falls.

### Chapter 3: MapReduce Programming Model

11. **Q:** What is MapReduce?
11. **A:** MapReduce is the process / programming model which works with 3 parts, mapping the data - changing / transforming / counting with the data, then shuffle where we move data with the same keys to the same nodes and then the reduce where we reduce all the results from the map to a single result (could be many key value pairs), Map reduce allows for batch parrallel processing.
Map reduce is implemented by implementing 2 functions, the Mapping function and the Reducing function, the mapping function transforms the data and makes aggregations or some other analysis on the data and returns key value pairs.
the Reduce function takes key value pairs and reduces them by key (example is counting or adding values for the same keys) to a single result which can have multiple key value pairs with no duplicate keys.
mapreduce was introduced in 2004 to allow for large scale distributed computing.
Map reduce works by running the map part on all machines with data, then shuffling the data according to the keys and then reducing, all happening on as many machines as possible on the cluster in parrallel to lower the time of processing.
the reducing part happens on the same machines that did the mapping part so that less data will be moved.
mapreduce has simplified data processing on large clusters.
the main benefits of mapreduce is that it allows for parallel computing on large clusters with ease without moving data too much and it allows to do almost all needed analyzations on the data and is very scaleable and easy to design and schedual.
the main draw back is that mapredce is very rigid, meaning that the only thing we can do with it is mapping and then reducing data to a single result.
Map reduce integrates with hadoop using hadoop-mapreduce which is a framework for running mapreduce on top of an hdfs cluster.
the mapreduce framework consists of one Job tracker node (one per cluster) and one Task tracker per cluster node which manage the running of the map reduce functions.
after creating the mapreduce functions we can use the next command to run it:

```bash
bin/hadoop jar /usr/useName/COMPILED_JAR_NAMR.jar java.package.path /usr/userName/input/directory /usr/userName/output/directory
```
which will use the Job tracker to start this job which will call the task trackers to start these tasks on each node


12. **Q:** What is the role of a Mapper in MapReduce?
13. **A:** The mapper maps or changes the data on the machines, this is the part where we can transform the data and change it so that when reduced, it can be analyzed.
gets inputs as key value pairs, transforms and returns key value pairs as well or nothing / null.
the reducer is the one that chooses the grouping, can be set in java using an outputKeyComparator class, and the way the values get aggregated is using the Combiner class in java.

13. **Q:** What is the role of a Reducer in MapReduce?
14. **A:** The reducer shuffles and reduces the data from a lot of results to a single result (aggregates all the data into a single result which can be more than one key value pair).
The reducer takes the same key results and aggregates them into one result, multiple same-key, value pairs get transformed into a single key value pair.
the reducer also sorts first by keys so that all key-value pairs go to the same machine and then also sorts then by value.

14. **Q:** What is meant by "Shuffling" in MapReduce?
14. **A:** Moving the results from the map such that results with the same keys end up in the same node and assigning a reducer to the result, shuffling is done by 2 sorts, one sort by the key and the other sort by the value.
the first sort happens between workers meaning data is moved between workers, and the second shuffle is done inside the node after the first shuffle.

15. **Q:** Can a MapReduce job have zero Reducers?
15. **A:** Yes, the reducer part of the Mapreduce is optional, not all works require reducing, an example is converting formats, we would like to map the data but wont need to reduce it.

source:
https://www.databricks.com/glossary/mapreduce#:~:text=Unlike%20the%20map%20function%20which,the%20reduce%20function%20is%20optional.

### Chapter 4: Hadoop YARN

16. **Q:** What is YARN?
17. **Q:** What are the main components of YARN?
18. **Q:** What is the Resource Manager in YARN?
19. **Q:** What is the role of the Node Manager in YARN?
20. **Q:** How does YARN provide fault tolerance?

### Chapter 5: Apache Hive

21. **Q:** What is Apache Hive?
22. **Q:** What is the Hive Metastore?
23. **Q:** What is HiveQL?
24. **Q:** What are partitions in Hive?
25. **Q:** Can you define SerDe in the context of Hive?

### Chapter 6: Apache ZooKeeper

26. **Q:** What is Apache ZooKeeper and what role does it play in a distributed environment?
26. **A:** Zookeeper is a distributed configuration manager  and coordinator that holds different configurations for different systems which allows different systems to coordinate with each other and allows for a single source of  truth for configuration.
Zookeeper allows to coordinate between different nodes on a distributed system, allows for rolling configuration changes and helps in leader election and distributed locks.
Zookeeper also provides functionality of failover recovery and automatic leader election

27. **Q:** Can you explain the concept of znodes in ZooKeeper?
27. **A:** ZNodes are Nodes which store data, are similiar to files and directories, they can be used to store data in a distributed system. z nodes contain data and the version of the data to allow for versioning and also include timestamps for cache validation.

28. **Q:** How does ZooKeeper handle coordination and configuration management across distributed systems?
28. **A:** Zookeeper handles coordination and configuration management using watches (watches are a mechanism that allows sending notifications to clients through pushing and not pulling, to which the clients whome are subscribed can react accordingly) where clients can listen to changes, and atomicity (every action is atomic, meaning that there could be no race conditions and every action is either finished fully or not done at all) and sessions (client connect to the zookeeper server using sessions which are connections that are kept alive using heartbeats which are sent in fixed intervals which are configured using the zookeeper.connection.timeout.ms configuration option) which aid in the process of the coordination
Zookeeper uses a shared hirarchiel namespace and znodes to create a system similiar to a file system which allows for coordination between the distributed nodes
Zookeeper exposes a naming service which allows to identify nodes by name, similiar to a dns but for nodes in a distributed system, this helps nodes coordinate by simplifying the process of node discovery.
Zookeeper also include cluster management which include the status of the nodes in the cluster in real time.
Leader election by using ephermal nodes and watches, using a session that creates the ephermal node (a node alive while the session is active) and sending notifications to the system when the current leader dies/becomes unavaliable.
Locking and syncronization - zookeeper also exposes a locking and a syncronization service which allows for distributed locking (for data modification and could also be used for almost instant standby service takeover) and syncronize between processes that use the same resourceds.
Zookeeper also has a highly reliable data registry, meaning that even if some nodes fail, the data is still available through the use of data redundency.


29. **Q:** What are ephemeral nodes and sequence nodes in ZooKeeper, and how are they used?
29. **A:** *ephermal nodes* are nodes which last for as long as the session is kept alive which are often used used for master / leader allocation with a watch, where the system watches the ephermal node and if it goes down, the system gets a notification and knows it needs to reelect a leader, each ephermal node exists because of a session and per session there can only be one node and *sequence nodes* are nodes which have an assigned unique number, can be used for distributed counters, a use case can be web analytics like visit count and or track interactions of a user with our app (could be likes/serches/posts/comments).
there can be only one sequence node with a specific id and there cannot be nodes with duplicate id's
we can use ephermal nodes and sequence nodes at the same time, there could also be a sequence node that is also an ephermal node.


30. **Q:** How does ZooKeeper ensure data consistency and reliability across distributed nodes?
30. **A:** Zookeeper ensures consistency and reliability by replication and only the primary node being the one interacted with, in adition to atomicity.
Zookeeper ensured data consistency by using Atomicity, meaning that all operations either fully complete or don't complete at all, which prevents data races making the data consistant between all nodes (there won't be a situation when one node is updating data and another one is reading and so data is not consistant between reads)
Zookeeper also allows for leader election in distributed systems by using ephermal nodes and watches to elect new leaders when the current leader dies, it notifies the system through the watch that the leader has dies so it knows it needs to re-elect a leader (to re-elect a leadet there needs to be a majority of the cluster for the cluster to be running and be able to elect a new leader).
Zookeeper also knows how to handle a split brain condition, a split brain condidtion is when a cluster gets divided by a connection getting cutoff, the cluster is split and the leader stays on one of the clusters (either the 'left' or the 'right' cluster), if the leader was on the cluster with the majority of the system, that part of the cluster works as it worked before without any interference other than maybe some latency increase, and when the connection goes back, the nodes connect and syncronize with the leader.
in the case where the leader is not on the part with the majority (lets call it the left part), a leader re-election happens in the majority part (which we will name the right part) and the cluster is working as it was but might be desynchronized from the leader, however the right part of the cluster re elects a leader and works as it did before with possible data loss, after the clusters reconnect, a new leader election happens with the whole cluster and it keeps working as it worked before.

in both cases, the left cluster gets stuck in leader election and does not accept client connections which means that the left part is down.
    
##i Chapter 7: Apache HBase

31. **Q:** What is Apache HBase?
32. **Q:** What is a Row Key in HBase?
33. **Q:** What is a Column Family in HBase?
34. **Q:** How does HBase ensure data availability and fault tolerance?
35. **Q:** What is the role of ZooKeeper in an HBase environment?

### Chapter 8: Apache Kafka

36. **Q:** What is Apache Kafka?
36. **A:** Kafka is a distributed, replicated Streaming pub sub model which allows for event driven and event streaming architecture.
Kafka has a few main parts in it's architecture, the first being the the kafka broker (or a kafka server) and a kafka controller which is one of the kafka brokers in the cluster, only one active controller exits in a cluster at any given time, it is elected using the zookeeper ephermal nodes, each broker tries to create an ephermal node and the first one to create the node, aquires a lock and all the other brokers that didn't aquire the lock, bring the ephermal node down.
the kafka controller is responsible for the states of partitions and replicas, assigning partition leaders (are the partitions from which all the other brokers copy the data from that partition), monitoring the cluster (knowing which brokers are up and re-electing a leader as needed).
the kafka brokers are managing the topics and the partitions which allow to read (consume) and write (publish) data to the partitions which are queues.
kafka works by saving all the data on persistant disks while maintaining high throughput and low latency, it does it by using batching of data, sequential disk reads (which are reads that happen on disk where the data is stored sequentially meaning one after the other, this is done to minimize disk seek which can take up to 10 ms, and also because sequential disk reads on regular hdd's have speeds of 600MB/s where random disk reads can be as slow as 10 kb/s which is way slower) and utilizing the os pagecache and minimum byte copies along with batching to allow for high throughput and fast operations.
kafka works in an exactly once model meaning that each message is delivered exactly once and processed *exactly once*, the other ways kafka can work is with the at least once which is used for failover when a node reads and falls before processing and acknoledging the read and *at most once* which means that some data might be lost but data is processed at most one time or never.


37. **Q:** What are Topics in Kafka?
37. **A:** Topics in kafka are a way to logically divide data and different event types or events of streams to different names, kafka topics are built with partitions which are queues that hold tha data and allow to read them, however, unlike a regular queue, after data is read, it is not deleted.

38. **Q:** What are Partitions in Kafka?
38. **A:** Partitions in kafka are a single queue which contain data inside of them, only one consumer can be connected to the same partition, which is a part of a consumer group, a consumer group is a group of multiple kafka consumers which consume the same data, can be multiple replicas of a microservice that all read from the partition, in kafka, the offset of the reader from the partition is stored per consumer group, topic and partition as a single number, in order to guarantee exactly once delivery.


39. **Q:** What is the role of a Broker in Kafka?
39. **A:** The broker in kafka decides to which partition you will write or read and assigns partitions and stores data across multiple partitions (A kafka instance).
The broker stores the offset of the reading and sends the consumer the needed messages from the topic, when publishing, the broker chooses to which partition the data will go according to the key (similiar to hash load balancing) (the broker is to whom you publish or read the data from).
when producer published the data, he connects to a broker for a specific topic, the broker then decides to which partrition to write the message according to the key of the data, then the consumer can request the messages (or subscribe with a long poll), the broker checks the offset of the consumer group the consumer connected with to the broker and sends the data according to the offset and then the client recieves the data (usually the data is compressed when the producer sends the data and decompressed when the consumer reads the data in order to reduce network load).
Kafka also allows the use of acknoledgmentes, where after the data is sent, we wait for all the In Sync Nodes or ISR to receive the replica and send an ack to the replica leader, it sends an ack to the producer and also has acknoledgmentes to the consumer, where the consumer can either send the ack after data processing before the storing or after the storing before the processing which give us at most once and at least once uses respectively.


40. **Q:** What is the difference between a Kafka Producer and a Consumer?
40. **A:** kafka producer can only write data to the topic while a consumer reads data from the topic.
the producer writes to a topic and the broker decides to which partition it goes according to the key, and the consumer reads from a specific partition as a part of a consumer group, which share the same offset for reading from the topic, each consumer is assigned one partition, meaning only one consumer group can read from a partition, the partition is assigned to a consumer group by lexographical order.


### Chapter 10: Apache Impala

41. **Q:** What is Apache Impala?
42. **Q:** What is an Impala Daemon?
43. **Q:** What is the role of a Catalog Service in Impala?
44. **Q:** What is the role of a Query Coordinator in Impala?
45. **Q:** What is the difference between Refresh and Invalidate in Impala?

### Chapter 11: Partitioning

46. **Q:** What is Partitioning in databases and data storage?
47. **Q:** What are some common partitioning criteria?
48. **Q:** What is a Partition Key?
49. **Q:** Can you explain Partition Pruning?
50. **Q:** How is datetime-based partitioning used in real-world scenarios?

### Chapter 12: Kerberos Authentication

AS - Authenticating server
TGS - Ticket granting server
TGT - Ticket granting ticket
KDC - Key distribution center


51. **Q:** What is the primary purpose of the Key Distribution Center (KDC) in the Kerberos authentication system, and what are its two main components?
51. **A:** The key distribution center primary purpose is to authenticate a user and to grant him a TGT and a session key, the 2 main componenes are the authenticating server and the ticket granting server which grants the tgt, in addition there is the db which saves the tgt and the user data.
The process of authenticating a user has 6 steps:

- Initial client auth request: the user asks for his TGT, here no sensitive info is sent so the data is not encrypted, the AS checks with the KDC if the user exists and if it is it retrieves the users private key.

- Verification of client credentials: if the user does not exist, the authentication process stops here, if the username is found, the AS sends back the TGT fromn the TGS which is encrypted with the TGS secret key and the encrypted session key which it generated.

- Message decryption: the client uses the user hash or the secret key to extract the the TGT and the session key.

- Request for access with the TGT: The client requests from the TGS a service ticket using the TGT and sends the service ticket if the client has the permissions to acess the service.

- Application server request: The client sends the request to the service it wants to access with the service ticket recieved in pt. 4, if the service authenticates the request, the client can access the service.

- Application server response: If the client requsts the server to authenticate itself, in this step, the server decrypts the session key using it's secret key and then the session key decrypts the service ticket to ensure that both the client and the server are authenticated and then the server sends a authenticated and then the server sends a response to the client that both are authenticated



52. **Q:** How does the "kinit" command contribute to the Kerberos authentication process, and what does it allow users to obtain?
52. **A:** Kinit is used to get (or renew) the TGT from the KDC, it allows users to obtain the TGT from the Principal (a string containing the username and possibly the realm and looks like so: username@realm, it is what kerberos uses to authenticate users).
kinit will initialize the credentials cache and the Principal, if you do not provide a principal and use the -s flag, then the cached principal will be used.
if you give the cache a name with the -c flag, the cache will be saved and can be used later on, otherwise, the default cache will be used.


53. **Q:** Explain the concept of "Single Sign-On (SSO)" in the context of Kerberos authentication and its benefits for users.
53. **A:** Single sign on is a concept that allows a user to use one password to connect to multiple services, it benefits users by not having to remember a password for each service and instead using the same password for multiple services.
in kerberos, it means that you can use one TGT to get other service tickets and access those services if you are allowed without having to reauthenticate with each service you interact with.

54. **Q:** Why is the concept of "time sensitivity" important in Kerberos authentication, and how does it enhance security?
54. **A:** Time sensitivity is important to kerberos because it makes it so that even if someone steals the TGT, It will only be active for a short time and not minimize the damage that can be done.
It is implemented by the tickets having an expiration data and users having to authenticate with the service every time before interacting, so if the TGT expires, the user has to either renew the TGT using the kinit command or re authenticate.
the expiration of the ticket can be viewed from the cache using the ```bash klist -c``` command where it will be shown, or in the TGT file.

55. **Q:** In what real-world scenarios or use cases is Kerberos authentication commonly employed, and how does it contribute to security and ease of use in those contexts?
55. **A:** Windows authentication is using kerberos as it's base, Network security (AD of windows is also based on Kerberos), Some distributed systems (like hadoop) use kerberos to securely transfer data and to keept the data secure, and single sign on services often use kerberos.
Kerberos is also used in hadoop to keep the data encrypted and secured in motion and when stationary (with authenticated access only).
because hadoop is one of the largest distributed systems (can have a lot of nodes) which need to constantly communicate with each other, it means that all those nodes need to call the TGS and the AS constantly to get tokens to be able to talk between one another which can cause latency and a lot of traffic in the cluster which may slow down the system.
So to combat this, hadoop has built it's own layer over kerberos, called hadoop tokens which are granted by hadoop serices.
an example is the namenode which when a request needs read access to a block, the namenode grants a token which allows the caller to access thoses block, when trying to access the block, the caller needs to include all the tokens for all the blocks he wants to read.
The block tokens don't contain data about the principa from which they query the data or the Principal, instead they just say that the caller has access to a specific block.


### Chapter 13: Oozie Workflow Scheduler

56. **Q:** What is Apache Oozie, and how does it facilitate job scheduling and workflow management in a Hadoop environment?
57. **Q:** Can you differentiate between an Oozie Workflow job and a Coordinator job? Provide an example of when you would use each.
58. **Q:** Describe the lifecycle of an Oozie job. What are the typical states an Oozie job can be in, and what are the implications of each state?
59. **Q:** How does Oozie support SLA (Service Level Agreement) monitoring, and why is it important in managing data processing jobs?
60. **Q:** What are the main components of an Oozie Workflow job, and what is the role of each component?

## SKILA :pinched_fingers: :boxing_glove:
- The mentors will ask you qustions from their experience, prepare yourself to answer them.

## Wrapping Up :hourglass_flowing_sand:
Discuss your answers with your mentor and seek feedback on your understanding of the Hadoop ecosystem. Reflect on the areas where you need to improve and make a plan to strengthen your knowledge in those areas. Tomorrow, you will have the opportunity to present your research findings to the team, so make sure to prepare your presentation and be ready to share your insights.
