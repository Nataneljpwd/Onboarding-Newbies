### Answers to questions from first skila

1. **Q:** What are the disadvantages of Scaling out?
1. **A:** The disadvantages of scaling out are:
    - Expensive: scaling out is more expensive because we need to buy more machines which might be cheaper than upgrading an existing one.
    - Storage: scaling out can take a lot of space because we need physical space for all the machines.
    - Complexity: when scaling out, we need to manage all of our machines rather than managing just one or single digit machines.

2. **Q:** When are edit logs deleted?
2. **A:** Edit logs are deleted when:
    - a name node restarts.
    - when the secondary name node reconstructs the FSimage with the edit logs.
    - when the log is no longer needed (i.e was processed).

3. **Q:** What are the use cases where we have a map but not a reduce job?
3. **A:** There are a few such use cases, which include:
    - Data cleanup: when cleaning up data, we need to know whether we delete it or not, and we don't need the result of the map function later.
    - Data classification: when using a classifier, we map the data to run on the classifier and then load it without the need for a reduce.
    - Data converter: when converting data, lets say from celcius to fahrenheit or converting words to their respective length.
    - Data copying or syncing: when we copy data in parrallel, we run map jobs across the cluster without any reduce jobs, and example is distcp.

4. **Q:** What is an audit log and what audit logs are saved in hdfs?
4. **A:** Audit logs record the occurance of an event, the time of the event, the user who caused the event and the affected entity.
          Audit logs record events of administration activity, data access and modification, user denial or login failure and system wide changes.


5. **Q:** What is a rack?
5. **A:** A rack is a physical rack on which servers are placed, sometimes rack provide power distribution units, it is used to organize the servers and the connections between them, big server racks might include a single switch for all the servers, but some server racks may include one switch shared with another rack.


6. **Q:** What are the uses of the fsck command in hdfs?
6. **A:** The uses of the fsck include:
    - Preforming a file system check: it allows to check the file system and find corrupred / under/over/miss replicated blocks which tells the namenode that these blocks need to be dealt with.
    - Moving or deleting files.
    - Finding the blocks of a file and their locations.


7. **Q:** What is the name of the process of building the fsimage from the edit logs?
7. **A:** Checkpointing.


8. **Q:** What type of zookeeper node is used to create a lock? (i.e for leader election)
8. **A:** The type of node is a sequential ephermal node, the lock holder is the client that has the lowest ephermal sequential node number.


9. **Q:** What happens first during failover, the lock being aquired ot the node becoming active?
9. **A:** First the lock gets aquired by the zkfc because the previous ephermal sequential node gets deleted so the lock automatically goes to the next zkfc in line.


10. **Q:** What happens with corrupted blocks?
10. **A:** When a corrupted block is detected, the namenode checks if it has good replicas which are not corrupted, if the exist the namenode scheduales a replication for the block, after the replication, the corrupted block gets deleted, in the case where all blocks are corrupted, when trying to read the blocks, we will not be able to read the file and will get a missing block exception, the file won't be deleted until we decide to delete it.


11. **Q:** How do journal nodes stay synced?
11. **A:** When the NN writes to all the journal nodes, the edit logs are written to all the journal nodes but an acknoledgement from the majority is awaited, if one journal node goes out of sync, it will notice that it has missing transaction id's or a lower transaction id than the other JN's, and then the JN that is out of sync, will power down itself, then the QJM recovers the missing transactions from another JN that is up to date and then the JN is started again.


12. **Q:** When will a NN enter safe mode?
12. **A:** There are several reasons that a NN might enter safe mode, those reasons are:
    - Available space on disk is less than the required amount for storage (which is configured using the dfs.namenode.resource.du.reserved config)..
    - The NN can't load the FSImage and editlogs into memory.
    - The NN didn't recieve block reports from the datanodes.
    - There are many under replicated blocks or missing blocks.
    - To preform administration work like saving the current FS to persistant disk.
    
13. **Q:** What is truncate?
13. **A:** Truncate is the act of shortening (or reducing) something or deleting it's content, like a file, i.e truncating a file means that we are reducing the size of the file or clearing the files contents.


14. **Q:** What is the hadoop dfsadmin command used for in hdfs?
14. **A:** The hadoop dfsadmin command is used for performing administration work on the file system, examples include (and are not limited with):
    - Enter / exit / force exit / get status of safe mode in the NN.
    - Getting a report of the filesystem information (like raw disk usage) and node status (alive / dead / slow / decommisioning or decommisioned / entering maintnance).
    - Creating a namespace snapshot.
    - Upgrade / rollback a version.
    - Refresh nodes.
    - Print topology.
    - Get the fsimage or trigger block reports.


15. **Q:** What are miss replicated blocks?
15. **A:** Miss replicated blocks are blocks that are distributed not according to the hdfs rules (the rack awareness rules) which means that all replicas of the blocks are on the same rack.


16. **Q:** What is a decommisioned node or the decommisioning process?
16. **A:** The decommisioning process is the process where a node is being prepared for a long period of maintnance, and all of the blocks in the node get replicated to other DN's, this process might take a long time (days / weeks or months) depending on the count and size of blocks on the node, and a decommisioned node is a node that is prepared for long time maintnance and is not servinb requests and no read operations are done on it (like a temporary black list) and it is done by adding the node jhost to the dfs.hosts.exclude property in the hdfs site and than refreshing the nodes (hadoop dfsadmin -refreshNodes).


17. **Q:** What is a Hadoop hdfs snapshot and how does it protect us from data loss?
17. **A:** Snapshots in hadoop are a "snapshot" of the file system or read only copies of the entire file system or a secific subtree structure, snapshots protect us by enabling a "soft delete", meaning that when the file is deleted, it is not actually deleted but rather only the metadata in the NN about that file is deleted and in the FSimage, and the file itself still exists if it were inside the snapshot, the file still exists on the DN's but is not accesible because it does not exist in the FSImage or the NN metadata, and it is possible to recover by loading the snapshot to memory of the NN thus allowing access to the blocks of the file and thus to the file.


18. **Q:** What is SSSD?
18. **A:** SSSD or System Security Services Daemon is a system service that allows to access remote directories and authentication mechanims.
    It allows to enroll a machine into an AD or LDAP domain for authentication and authorization mechanisms.


19. **Q:** What kind of authentication tokens are used with hadoop and kerberos?
19. **A:** There are 2 types of tokens in kerberos and hadoop which are special to hadoop:
    - Block Access Token: A block token is given by the NN and it allows access to a specific block, without requiring to re-authenticate with kerberos to get a service ticket to each DN which reduces the load on the KDC in a distributed environment.
    - Delegation Token: A token that is a "two party" protocol (meaning it includes only the client and the server unlike kerberos which is a 3 party, where the client first authenticates with kerberos and then with the service) where the client and server authenticate using the delegation token.
    This token allows for access to services that issued the delegation token, and renewal is done with the service that granted it.
    The delegation token is usually passed to the services which run a job the client requested (like to YARN) in order to be able to run jobs and access services on the behalf of the client or in other words, the client 'delegates' it's credentials to those services, from this process comes the name of the token.


20. **Q:** What is the size of a block report? and is it sent in one part?
20. **A:** The size of a block report differs depending on the amount of blocks the DN contains, the block report consists of 4 parts:

    - Datanode Registration: includes the DN registration information (size: 4 bytes)
    - Block Pool ID: A string that represents the block pool ID of the reported blocks (or the id of the blocks that are under a certain namespace) (size: 13 bytes + 4 to 12 bytes (ip of DN) + 14 bytes assuming ascii encoding, total: 31 to 39 bytes)
    - Storage Block Report: an array of longs which represent the blocks that are reported, each chunk of 4 longs represent a block, the first long represents the block id, the second represents the length of the block, the third is a generation timestamp and the fourth represents the replica state if theblock is under construction , it is repeated as the amount of blocks (size: 32 bytes * amount of blocks)
    - Block Report Context (Optional): includes the amount of RPC requests the BR is split to (int32), the index of the current BR (int32), the id of the block report (long) and the lease id (optional) (size: 16 to 24 bytes).

    and so the block size varies from a minimum of 67 bytes and up (if only one block reported and ip is only single digit numbers), and it can be large at times so it can be split to multiple rpc requests (as can be understood from the rpc requests count).


21. **Q:** Where is the metadata of files stored and what is the blk_{blk-id}.meta file?
21. **A:** The metadata of files are all stored in the NN in memory and on the FSImage, and the .meta file includes the checksum of the block.


22. **Q:** Why are small files bad in hdfs?
22. **A:** Small files are bad in hdfs because for each block we save, we need to store the metadata in the NN, which in turn can cause an out of memory exception if too many small files are used while the utilization of the cluster is pretty low, when having a lot of small files, the NN starts limiting us way more than the DN's as the ram gets overused while the DN's storage is barely used.
    In addition, HDFS is not made to access small files efficiently as it was designed to give stream access to very large files through reading smaller files, when saving small files, a lot of disk seeks happen which slow down the cluster significantly, especially that hdfs was designed to run on comodety hardware that might not have the fastest seek times or good random read performance.
    When using Mapreduce, a map task is spawned for each block, if we have a lot of small files rather than a big file split into 128 MB blocks, the we can have 10's to 100's of times more map tasks which will excecute way slower because there are not enough nodes so a lot of bookeeping is done and way more schedualing needs to be done by YARN (or Job tracker in older versions), in addition to having to start a new JVM for each input split (but it can be avoided by using the mapred.job.reuse.jvm.num.tasks option ansd the MultiFileInputSplit class in the mapreduce job to run multiple inputs on the same task).


23. **Q:** How does the prod architecture of CDH look like?
23. **A:** [Diagram](https://drive.google.com/file/d/1ZmeJL-aCzi7ba4YcqsZmRDmffvd7Ym61/view?usp=drive_link)


24. **Q:** What is fencing and how does it happen in hadoop?
24. **A:** Fencing is the process of isolating a node that might be mis-behaving or doing things that it is not supposed to do, i.e:
    - A NN leader election is caused because of network latency which caused a leader re election, while the now active NN still thinks it is the active NN while a new leader has been elected, the previously active NN gets fenced by the JN (as only one writer can exist) and using ssh fencing or nfs fencing to fence away the NN by killing the process, so that it won't serve clients and won't cause any corruption or interfere with the current active NN.


25. **Q:** What is a kerberos realm?
25. **A:** A kerberos realm is a logial grouping (or network) of principals that represent an administrative domain or group that are under the same master KDC.
    Kerberos realms can be hierarchial meaning one is a super set of the other realm (the mapping between them must be defined by creating a shared principal between the 2 realms called krbtgt/REALM.NAME.ONE@REALM.NAME.TWO using the kadmin command and create the principals with the same password), otherwise they are direct or not hierarchial.
    Kerberos permits cross-realm authentication which is done by only having a principal entry for the other realm in it's master KDC (for both realms).


26. **Q:** When do we need and when don't we need a password in kerberos?
26. **A:** A password is needed in kerberos each time the tgt expires and needs to be renewd or when loging in using the kinit command, however, we don't need to enter the password when we access a different service that we have access to because we call the TGS to get the service ticket for the specific service we want to access using our TGT.


27. **Q:** What happens during NN startup?
27. **A:** When a NN starts, the first thing it does is load the fsimage to memory and apply the edits from the edit logs, once it has reconstructed the fsimage, it creates a new updated fsimage file (or checkpointing) and empties the edit logs, during this process, the NN is running in safe mode, meaning that it is in a readonly mode to the clients, during this mode, any block replication stops until it knows about a certain amount of blocks (defualt is 99.9%) that are replicated enough (have above the dfs.namenode.replication.min amount of replicas), and after 30 seconds and it has a 99.9% blocks that are replicated enough, it exists safe mode and scheduales the under or miss replicated blocks for replication as well as taking count of the missing and currupted blocks. 
