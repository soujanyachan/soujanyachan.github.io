link: https://www.youtube.com/watch?v=R873BlNVUB4
name: apache kafka crash course
topic:
author:
tags:
github:
creation date: 2021-08-02 13:51

[[kafka]]
[[cs_learning]]

tcp connection bw producer and broker (server)
topic is a logical partitioning of data

consumer polls for info (unlike rabbitmq where server pushes to the consumer)

if topic grows large we need 'sharding', kafka has borrowed the concept and has created partitions

queue - pub once, consumed once
pubsub - message published once, consumed many times

kafka was designed with both q and pubsub 

consumer groups were created for parallel processing in partitions
each partition needs to be consumed by some consumer.

to act like a queue put all consumers into one group

for pub sub, each consumer in a unique group

distribution -> another broker, 
copy partitions and mark one as leader and follower but how to know.
can have partition level leader and follower

zookeeper ->
- handles the leader follower consensus for each partition

zookeeper gossip system ?

pros
- append only commit log (write once read many)
- good performance
- distributed
- long polling - 
- event driven, pub sub and a queue

cons
- zookeeper 
- explicit partition can lead to problems (vitess)