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

1. **Q:** What is Apache Hadoop?
1. **A:** Hadoop is a distributed file system that works based on a master-slave architecture which was built with the assumption that hardware failure is the norm.

2. **Q:** Can you name a few vendor-specific distributions of Hadoop?
2. **A:** Cloudera Distribution Platform, Amazon Elastic MapReduce, Microsoft azure HDInsight.

3. **Q:** What are the three modes in which Hadoop can run?
3. **A:** **Standalone (default)** - where it runs as a single java process, **Psuedo Distributed** - where there is a single node cluster (many processes on one machine) which simulates the real world but still runs on one machine which is used to test and debug, **distributed** - a multi node cluster which includes the Namenode, Secondary Namenode and the Datanodes.

4. **Q:** What is the primary role of the `hadoop-env.sh` configuration file?
4. **A:** the primary role is to setup hadoop process and other java-related processes like memory for the java process.

5. **Q:** What purpose does the `core-site.xml` file serve?
5. **A:** The purpose of the core site is to configure mostly IO related things and also the filesystem and network addresses.

### Chapter 2: Hadoop Distributed File System (HDFS)

6. **Q:** What is HDFS?
6. **A:** HDFS is the Hadoop distributed system which is basically like a regular file system but it is distributed between multiple computers.

7. **Q:** What is the role of the NameNode in HDFS?
7. **A:** The role of the NameNode is to save metadata about the file and to manage where they are saved, in addition to managing and saving the FS structure and also replicate / delete replications as needed.

8. **Q:** What is a DataNode in HDFS?
8. **A:** A DataNode is the node that saves the data itself in the form of blocks with a max size that was configured beforehand in the hdfs-site.

9. **Q:** How does HDFS achieve fault tolerance?
9. **A:** Hdfs achieves fault tolorence by using redundency, replication and rack awareness, in addition to journal nodes and secondary namenode and more.

10. **Q:** Can you explain rack awareness in HDFS?
10. **A:** Rack awareness means that hadoop knows the physical network topology of the network, which allows hadoop to distribute the files such that even if a rack crashed, the data is still available.

### Chapter 3: MapReduce Programming Model

11. **Q:** What is MapReduce?
11. **A:** MapReduce is the process / programming model which works with 3 parts, mapping the data - changing / transforming / counting with the data, then shuffle where we move data with the same keys to the same nodes and then the reduce where we reduce all the results from the map to a single result, Map reduce allows for batch parrallel processing.

12. **Q:** What is the role of a Mapper in MapReduce?
12. **A:** The mapper maps or changes the data.

13. **Q:** What is the role of a Reducer in MapReduce?
13. **A:** The reducer shuffles and reduces the data from a lot of results to a single result (aggregates all the data into a single result).

14. **Q:** What is meant by "Shuffling" in MapReduce?
14. **A:** Moving the results from the map such that results with the same keys end up in the same node and assigning a reducer to the result.

15. **Q:** Can a MapReduce job have zero Reducers?
15. **A:** Yes, the reducer part of the Mapreduce is optional.

### Chapter 4: Hadoop YARN

16. **Q:** What is YARN?
16. **A:** YARN is a Resource negotiator and manager which allocates and manages resourses for processes or applications.

17. **Q:** What are the main components of YARN?
17. **A:** The main components of Yarn are the Resource manager which gives and also takes resources, Application manager which negotioates witht he resource manager for resources and the nodes or containers which are wher the process runs, and the Node manager which is a per machine instance that is responsible fot the containers, meaning monitoring them and reporting to the resource manager and schedualer.

18. **Q:** What is the Resource Manager in YARN?
18. **A:** The resource manager is the component that manages, allocates and takes resources.

19. **Q:** What is the role of the Node Manager in YARN?
19. **A:** The role of the node manager is to monitor and report the resource usage of the containers to the resource manager and schedualer, in addition it preforms health status updates.
 
20. **Q:** How does YARN provide fault tolerance?
20. **A:** Yarn provides fault tolorence by separating job schedualing and resource management from the data components, in addition to regular health checks and restarting failed containers.

### Chapter 5: Apache Hive

21. **Q:** What is Apache Hive?
21. **A:** Apache hive is a Data warehouse application which goes over hadoop and stores data as tables and allows for sql syntax queries.

22. **Q:** What is the Hive Metastore?
22. **A:** Hive Metastore is the centralized metadata repository that stores schema and partition information about the data.

23. **Q:** What is HiveQL?
23. **A:** Hiveql is a sql like query language that can be used to query on the data in hive.

24. **Q:** What are partitions in Hive?
24. **A:** Partitions are parts of the table split between machines used in case the tables are to big in order to distribute the processing and the data which in return speeds up the process of analyzing and querying on the data and for less data to be processed using pruning.

25. **Q:** Can you define SerDe in the context of Hive?
25. **A:** SerDe is the Serializer and the Deserializer which decides how hive stores and reads the data.

### Chapter 6: Apache ZooKeeper

26. **Q:** What is Apache ZooKeeper and what role does it play in a distributed environment?
26. **A:** Zookeeper is a distributed configuration manager  and coordinator that holds different configurations for different systems which allows different systems to coordinate with each other and allows for a single source of configuration change.

27. **Q:** Can you explain the concept of znodes in ZooKeeper?
27. **A:** ZNodes are Like data nodes which can have children, which in turn acts like files and directories.

28. **Q:** How does ZooKeeper handle coordination and configuration management across distributed systems?
28. **A:** Zookeeper handles coordination and configuration management using watches where clients can listen to changes, and atomicity and sessions which aid in the process of the coordination

29. **Q:** What are ephemeral nodes and sequence nodes in ZooKeeper, and how are they used?
29. **A:** *ephermal nodes* are nodes which last for as long as the session is kept alive which can be used for master / leader allocation and *sequence nodes* are nodes which have an assigned unique number, can be used for distributed counters.

30. **Q:** How does ZooKeeper ensure data consistency and reliability across distributed nodes?
30. **A:** Zookeeper ensures consistency and reliability by replication and only the primary node being the one interacted with, in adition to atomicity.

### Chapter 7: Apache HBase

31. **Q:** What is Apache HBase?
32. **Q:** What is a Row Key in HBase?
33. **Q:** What is a Column Family in HBase?
34. **Q:** How oes HBase ensure data availability and fault tolerance?
35. **Q:** What is the role of ZooKeeper in an HBase environment?

### Chapter 8: Apache Kafka

36. **Q:** What is Apache Kafka?
36. **A:** Kafka is a distributed, replicated Streaming pub sub model which allows for event driven and event streaming architecture.

37. **Q:** What are Topics in Kafka?
37. **A:** Topics in kafka are a way to organize data, a topic is like a queue of data (could be multiple queues for distributed purposes and for performance improvements) which we can subscribe or publish to.

38. **Q:** What are Partitions in Kafka?
38. **A:** Partitions in kafka are a single queue which contain data inside of them, only one consumer group can be connected to the same partition

39. **Q:** What is the role of a Broker in Kafka?
39. **A:** The broker in kafka decides to which partition you will write or read and assigns partitions and stores data across multiple partitions (A kafka instance).

40. **Q:** What is the difference between a Kafka Producer and a Consumer?
40. **A:** kafka producer can only write data to the topic while a consumer reads data from the topic.

### Chapter 10: Apache Impala

41. **Q:** What is Apache Impala?
42. **Q:** What is an Impala Daemon?
43. **Q:** What is the role of a Catalog Service in Impala?
44. **Q:** What is the role of a Query Coordinator in Impala?
45. **Q:** What is the difference between Refresh and Invalidate in Impala?

### Chapter 11: Partitioning

46. **Q:** What is Partitioning in databases and data storage?
46. **A:** Partitioning is a way to split data into multiple groups in order to query more effectively while pruning more data, partitioning is also used to distribute a database.

47. **Q:** What are some common partitioning criteria?
47. **A:** Range partitioning, List partitioning, composite partitioning, hash partitioning and round robin.

48. **Q:** What is a Partition Key?
48. **A:** partition key is the key according to which we partition the data which decides to which partition the record belongs.

49. **Q:** Can you explain Partition Pruning?
49. **A:** Partition pruning is when we search less data using the partitions, example, if we partition by date (default partition on many db's) and search for everything in the last year, we won't need to search through all the records that date years back and instead we will prune them and search only the partition which contains the last year.

50. **Q:** How is datetime-based partitioning used in real-world scenarios?
50. **A:** Datetime based partitioning is the default partitioning method on many databases, an example for real world use is timescaleDB which is a superset of postgresql which partitions based on datetime with compression and additional indexing by datetime which allows for very fast time series data analysis


### Chapter 12: Kerberos Authentication

51. **Q:** What is the primary purpose of the Key Distribution Center (KDC) in the Kerberos authentication system, and what are its two main components?
51. **A:** The key distribution center primary purpose is to authenticate a user and to grant him a TGT and a session key, the 2 main componenes are the authenticating server and the ticket granting server which grants the tgt, in addition there is the db which saves the tgt and the user data

52. **Q:** How does the "kinit" command contribute to the Kerberos authentication process, and what does it allow users to obtain?
53. **Q:** Explain the concept of "Single Sign-On (SSO)" in the context of Kerberos authentication and its benefits for users.
54. **Q:** Why is the concept of "time sensitivity" important in Kerberos authentication, and how does it enhance security?
55. **Q:** In what real-world scenarios or use cases is Kerberos authentication commonly employed, and how does it contribute to security and ease of use in those contexts?

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
