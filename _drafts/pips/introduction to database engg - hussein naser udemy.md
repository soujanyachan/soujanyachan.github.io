## Intro to ACID
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

## primary key vs secondary key
- table spaces / heap & primary key
	- row store
	- area in disk is dedicated to expensive data, slow access
	- organised row by row, no ordering
	- clustering - organising a table around a key, ordering - additional cost
	- oracle - index organised table, or clustered index
	- heap is organised around that index
	- 