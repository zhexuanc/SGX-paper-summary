# SecureKeeper: Confidential ZooKeeper using Intel SGX
###### Stefan Brenner, Colin Wulf, David Goltzsche, Nico Weichbrodt, Matthias Lorenz, Christof Fetzer, Youjung Shin, Taesoo Kim, Brent Byunghoon, Kang Dongsu Han

**What's the problem?**
* Cloud computing needs trust for data. Third party cloud computing blocks are attached with potential sensitive application data. Also, the hardware security protection like Intel SGX provides useful function for these issues. How to use them correctly is a problem.

**Summary**
* This paper describes an enhanced version of zookeeper that uses SGX to protect the confidentiality and integrity of data.  SecureKeeper uses multiple small enclaves to ensure that (i) user-provided data in ZooKeeper is always kept encrypted while not residing inside an enclave, and (ii) essential processing steps that demand plaintext access can still be performed securely. 

**Key insight**
*  The total security guarantees of SecureKeeper are enforced through a integration of two enclave types: (i) an entry enclave is instantiated for each client and responsible for protecting the client-replica connection and the data security of the ZooKeeper data store; (ii) a counter enclave is instantiated only once at the leader replica of the ZooKeeper cluster, and handles special write requests of sequential nodes that perform data processing.

**Notable design details**
* In order to keep the data save, SecureKeeper takes a middle ground and stores and processes data in encrypted form where feasible and redirects plaintext processing to enclaves.
* To solve that memory demanding is really big in zookeeper, the authors implement SecureKeeper using tailored enclaves and only move critical code sections into enclaves, so that the memory is smaller when processing data.

**Limitations**
* The design part is seperate from SecureKeeper section, which is a little mess. Also, the implement is not that detailed.
* The defence of replay attack and DoS attack cannot be defended because one solution is Byzantine fault-tolerant agreement protocol but this requires significant changes to the ZooKeeper architecture, which is incompatible with the design goals of SecureKeeper.

**Summary of the key results**
* SecureKeeper demonstrates how tailored enclaves can be integrated minimal-invasively to ensure confidentiality of all managed user data and integrity for plain znodes.
* The protection of SecureKeeper keeps the security of all user provided data in zookeeper databases.

**Open questions**
* It can be assumed that other services that mostly handle data but do not process it can be protected similarly. Simple KVS and blob storage may be a good fit because they access data by a unique identifier.

