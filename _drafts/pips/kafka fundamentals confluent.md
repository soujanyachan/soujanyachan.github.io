[[cs_learning]]

producers (write, stored on broker disks)-> brokers <-(polls broker to read data) consumers

```mermaid
graph TD
id1(producer)
id2(brokers)
id3(consumer)

id4(zookeepers)
```

zookeepers are used for consensus on - distributed consensus manager
acl are stored in zk
when a broker fails, detection and recovery zk -> election of new leaders
cluster management

decouples producers and consumers
slow consumers do not affect producers
adding consumers without affecting producers
failure of consumer does not affect system


topic is a collection of related messages or events, its a durable log ie needs to be stored on disk. the broker that the partition lives on is just a computer and if r/w messages is happening there, can't scale forever.
so topics are broken into pieces, partitions are each allocated to a sepeate brokers

partition is similar to a log

ordering in partition is always there but not necessarily in topic
the partition is stored as multiple segments (similar to rolling files)

record
- key - string / int / compound serialised obj
- value - domain obj
- headers - metadata
- timestamp

broker responsibilites
- manage partitions
- takes ip from producers, updates partitions, gives op to consumers
- broker replication factor -> leader, followers


how does a producer know which partition to write a message to ?
- no key ? round robin
- key ? hash(key)%partitions i.e. messages with the same key go the same partition which means they are strictly ordered all the time

consumers poll, consumer offset that keeps track of the last message read is stored in a special topic named `consumer_offsets`

every consumer is a consumer group in kafka
