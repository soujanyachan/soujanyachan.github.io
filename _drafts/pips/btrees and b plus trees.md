name: btrees and b plus trees
topic:
author:
tags:
link: https://www.youtube.com/watch?v=aZjYr87r1b8

1. disk str
2. how data is stored on disk
3. indexing
4. multilevel indexing
5. m-way search trees
6. b trees
7. insertion and deletion
8. b+ trees

platter with logical circles called tracks
sectors
blocks
any loc on disk can be found by (track, sector)
block size is typically 512 bytes -> depends on manufacturers
any byte can be addressed (block address{track, sector}, offset)

data is always stored as block

main memory (RAM)
- data from disk needs to be put into main memory
- data structure -> org of data in the main mem
- dbms -> organisation of the data in the disk 

how data is stored on the disk in the form of database
- num of records per block = block size/ record size 
- what happens when you want to search 
	- time -> depends on num of block accesses
	- reduce time using index

index
- key and ptr to a record
- dense index
- index is also stored in disk only
- how much space will index take? (id + ptr) * num of records; blocks reqd = block size / total space taken by index
- total search space when index is used = space taken by index + one block for the record itself

multilevel index
- if index size also grows
- for each block of the lower level index there is an entry
- sparse index

self managed multilevel indexes

m-way search trees
- search tree in which each node has at most m children
- m -1 keys
- degree of node

4 - way search trees 
```
ptr | k1 | ptr | k2 | ptr | k3 | ptr -> node str
```

but we need record pointers also
```
___________________________________________________________________
| ptr | k1 (recptr) | ptr | k2 (recptr) | ptr | k3 (recptr) | ptr |
|_____|_____________|_____|_____________|_____|_____________|_____|
```

b trees
- worst case height of m-way search tree is go through all the nodes exactly like linear search
- m - way search trees with rules 
