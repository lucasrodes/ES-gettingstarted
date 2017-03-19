# Basics

## Introduction

- Is a document store
- Is incredibly fast when searching! Good scalability.
- whole goal: increase performance!
- Written in JAVA
- Distributed architecture
- Communication is done through HTTP REST API:
    - `curl -X <REST Verb> <Node>:<Port>/<Index>/<Type>/<ID>`
    - E.g. `curl -X GET http://localhost>9200/person/employee/123`
- Schema-less JSON documents (like NoSQL databases) => No need to define fields!
- Developed by ElasticSearch, Open Source

### Very popular

Wikimedia, Mozilla, Quora, Github, Netflix, Soundcloud

=> It scales amazingly good!

## Terminology

** Near Realtime (NRT) **

- Small latency from a document is indexed until it is searchable!
- This slight delay is due to the ditributed architecture of ES.
- For large clusters, the delay can be of 1s. Thats quite impressive.

** Cluster **

- It refers to a collection of nodes (servers)
- It might consist of several nodes, depending on the scale
- The collection of nodes contain the data of the collection
- The cluster provides indexing and search capability accross all nodes (you do not need to worry which node stores the document you are looking for)
- Identified by a unique name (defaults to "elasticsearch")

** Node **

- A single server that is part of a cluster
- Stores searchable data
    - If there is only one node, it stores all the data in the cluster. Otherwise, it stores part of the data.
- It participates in a clusters indexing and search capabilities. Nodes collaborate in a request!
- It is identified by a name
- A node joins a cluster named "elasticsearch" by default
- Starting a single node on a network will by default create a new single-node cluster named "elasticsearch"

** Index **
- Collection a documents (e.g. product, account, movie)
    - Each of the above exampels would be a _type_
- Corresponds to a database within a relational database system
- Identified by a name, which must be lowercased
    - Used when indexing, searching, updating and deleting documents within the index
- You can define as many indexes as you want within a cluster.

Brief: Think of it as a relational database.

** Type **

- Within an index there might be several types
- Represents a class/category of similar documents, e.g. "user"
- Consists of a name and a mapping
- Simplified you can thing of a type as a table within a relational database.
- An index can have one or more types defined, each with their own mapping.

** Mapping **

- Similar to a database schema for a table in a relational database
- Describes the fields that a document of a given type might have
    - Includes the data type for each field, e.g. string, integer, data,...
    - Also includes information on how fields should be indexed and stored by Lucene
- Dynamic mapping means that it is optional to define a mapping explicitly.

** Document **

- A basic unit of information that can be inxeded
- Consists of fields, which are key/value pars
    - A value can be a string, date, object, etc.
- Corresponds to an object in an object-oriented programming language
    - A document can be a single user, order, product, etc.
- Documents are expressed in JSON
- You can store as many documents within an index as you want

### Analogy with relational database

| ElasticSearch             | rel. database                 |
|:-------------------------:|:-----------------------------:|
| index                     | database                      |
| type                      | table                         |
| document                  | row in a database table       |
| fields of a document      | columns in a database table   |
| mapping                   | schema for a table            |

** Shards **

- An index can be divided into multiple pieces called shards
    - Useful if an index contains more data than the hardware of a node can store (e.g. 1TB data ona 500 GB disk)
- A shard is a fully functional and independent index
    - Can be stored on any node in a cluster
- The number of shards can be specified when creating an index
- Allows to scale horizontally by content volume
- Allows to distribute and parallelize operations accross shards, which increases performance.

** Replicas **

- Copy of a shard
- Provides high availability in case a shard or node fails
    - A replica never resides on the same node as the original shard
- Allows scaling search volume, because search queries can be executed on all replicas in parallel
- By default, ES adds 5 primary shards and 1 replica for each index.

