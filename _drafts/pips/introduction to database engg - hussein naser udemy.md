# Intro to ACID
- transaction - 
	- collection of queries
	- one unit of work
	- commit 
	- rollback
- A - atomicity - 
	- all of the queries should succeed.
	- even if one fails you need to rollback
- I - isolation -
	- inflight transaction cannot see changes by other transactions
	- read phenomena - 	
		- dirty read - read a value that wasnt committed (lock)
		- non repeatable reads - non idempotent read in the same transaction (lock)
		- phantom read - selecting but getting extra from some other transactions (new value cant lock - serialisation)
		- (lost updates) - changed a value and another transaction changed the same value, so you lost your update
	- isolation levels
		- read uncommitted - no isolation, any change from outside is visible
		- read committed - each query in a transaction only sees committed stuff at the time of the query
		- repeatable - each query in a transaction sees only committed updates at the beginning of the transaction - (implementation eg versioning in cassandra)
		- serialised - transactions cannot be executed in parallel, no isolation issues / concurrency issues
		- ![[Screenshot 2021-08-27 at 13.04.50.png]]
- C - consistency - atomicity and isolation lead to consistency
	- consistency in data (eg insta likes, youtube subs)
		- defined by user - table schema
		- referential integrity - foreign keys
		- atomicity
		- isolation
	- consistency in reading
		- if a transation committed a change will a new transaction immediately see the change?
		- both relational and nosql databases suffer from this 
		- replica lag between the different servers (eventual consistency)
- D - durability
	- committed transaction must be persisted in a durable non volatile storage
- eventual consistency
	- when nosql started to emerge
	- for both sql and nosql
	- if you introduce a cache, there is inconsistency in the whole system until cache is updated
- **postgres** prevents phantom reads even in repeatable read
- mvcc - multi version concurrency control
- either serialisable or pessimistic locking 

- serialisable vs non repeatable
	- dep when it comes to reading and writing and that can change the result then i need serialisable
		- engineer must be prepared for errors when there are dependencies bw transactions
	- non repeatable can still have issues

Since the crash happened during the commit the database cannot guarantee durability. The system is durable only when the commit is successful( the data is fully written to disk). That is why commit speeds are critical, the faster you can commit the lower the chances of such corruption.

# database indexing
## primary key vs secondary key
- table spaces / heap & primary key
	- row store
	- area in disk is dedicated to expensive data, slow access
	- organised row by row, no ordering
	- clustering - organising a table around a key, ordering - additional cost
	- oracle - index organised table, or clustered index
	- heap is organised around that index
	- speed for i/o esp range queries
	- if secondary index -> ie table is jumbled
	- guid is a bad idea to use as the primary key as we will not benefit from the memory caching that the db does
	- secondary -> has another structure outside the table for the indexes, heave to the heap to select the data, as the index does not contain all the data

## getting started with indexing
- btree
- lsm

index only scan
try to avoid the table as much as possible
db caching 
if it does not have an index, full table scan
postgres tries to do in parallel, multiple threads

like is the worst query, full scan -> expression matching requires
bitmap heap scan on employees

## explain in postgres
- query plan
- seq scan = full table scan
- cost = 0.00..289.15
	- first num -> time to fetch first page
		- increases if it does work before fetching
	- second num -> the estimated time to get all
	- rows -> approx num of rows
	- similarly to rows, width
- read from bottom to top

## index scan vs index only scan
- non key column -> just to store with the index
- not always good as it increases the size of the index
- key vs non key column db indexing
- vacuum verbose -> postgres

## combining database indexes for better performance
- index on a, index on b
- select c -> bitmap heap scan
- postgres - can scan values from the left
- multicolumn b-tree index can be used with queries that involve any subset of the index columns but the index is most efficient when the constraints are on the leading columns.

## how database optimisers decide which index to use
- both indexes and merges the result
- only one index instead of two, esp if one returns very few and the condition is an AND
- full scan with many workers
- ensure after large update, to update stats in db
- database hinting

## bitmap index scan vs index scan vs table scan
- array of bits, and the values rep the page num, 
- bitmapand 

## creating index concurrently - avoid blocking prod
- writes are blocked when creating an index
- create index conccurently - write also allowed during creation - postgres
- multiple scans much longer, more cpu, more mem
- potentially fails

## bloom filters
- to check whether something exists
- prevent unnecearry queries
- cassandra -> uses this internally

## working with billion row table
- how will the table grow ?
- for a big table
	- brute force your way, search in parallel
	- avoid processing the entire table, subset of the table only -> best is to use indexing
- sharding and parition keys

## btree vs b+ tree in prod
- full table scans
	- read all pages, many I/Os
	- need to reduce the search space
	- 
- b tree -> balanced tree,
- b tree limitations
- b+ tree
- b+ considering
- b+ tree storage cost in mysql vs postgres

## original btree
- balanced data str for fast traversal
- minimise the search space
- m degree some nodes can have m child nodes
- node has up to (m-1) elements
- each element has a key and a value
- value is a data pointer to the row
- ptr can pointer to primary key or to the tuple
- root, internal node, leaf node
- a node = disk page

## how does btree help performance
- easy search

## limitation b tree
 - elements in all nodes store both the key anf the value
 - internal nodes thake more space, require more io, slow down traversal
 - range queries are slow because of random access

b+ trees
- all data is pushed to leaves, only keys in internal nodes
- leaf nodes are linked -> good for range queries

## b+ tree dbms considerations
- leaf ptr is cheap
- 1 node fits dbms page
- can fit internal nodes in memory easily
- leaf nodes can live in data files in the heap

## b+ tree storage cost in mysql vs postgres
- secondary index values can either point to the tuple (pg) or primary key (mysql)
- if primary key data type is expensive this can cuse bloat in all secondary indexes such as mysql (innodb)
- leaf nodes in mysql (innodb) contains the full row since its an Index Organised Table / clustered index

## b tree summary
- full table scan
- b tree
- b tree limmitatino
- b+ trees
- b+ tree considerations
- b+ tree storage cost

## database partitioning
- what is partitioning - split up a table into multiple tables based on the where clause the db decided which sub table to hit
- horz adn vertical - 
- partitioning types
- partitioning vs sharding
- pros and cons

## vertical and horz partitioning
- horz
	- split by row - range or list
- vert partitioning splits by columns
	- large column that you can store in a slow access drive in its own table space

## partition types
- by range - date, id, log date, customer id
- by list - discrete values (like states - KA, AP)
- by hash - consistent hashing

## horz partitioning vs sharding
- HP splits big table into smaller tables in the same db , client is agnostic
- sharding splits big table into multiple tables across multiple db servers
- HP table name changes
- sharding everything is the same but the server changes

## postgres demo
- pg can create indexes for the paritions of the table

## ads and disads of partitions
- pros
	- imporves query performance when accessing a single partition
	- sequential scan vs scattered index scan
	- easy bulk loading ( attach partition)
	- archive old data into cheap storage

- cons
	- updating a row moves the row from one partition to another (slow or fail sometimes)
	- ineffiecient queries could scan all partitions
	- schema changes can be challenges (dbms could manage it)

## sharding
- scaling split across servers
- what is sharding
- consistent hashing - hash rank to find the db server to hit (eg. cassandra)
- horz partitioning vs sharding
- pros of sharding
	- scalability
		- data
		- memory
	- security -> only some users can access certain shards
	- optimal and smaller index size
- cons of sharding
	- complex client
	- transactions across shards
	- rollbacks
	- schema changes are hard
	- joins
	- you need to know what you are querying for otherwise you need to hit all

when to consider sharding?
- better not to complicate if simple app
- horz partitions
- replication
- two masters,(replication + sharding?)
- sharding

## concurrency control
- exclusive lock / write lock
	- only one person can update
	- there must not be any shared lock
- shared lock
	- read lock
	- no exclusive lock on the same data
- 