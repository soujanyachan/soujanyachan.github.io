
- strong and statically typed
	- strong typing - type of a variable cannot change over time
	- static typing - variable have to be defined at compile time
- tend to be verbose? compiler is well designed to prevent this
- strong community
- key features
	- simplicity
	- fast compile times
	- garbage collected - dont have to manage memory, (decrease garbage collection time)
	- concurrency is built in
	- compile to standalone binaries - versioning is easy
- resources
	- golang.org
	- [[Effective Go]]

# variables
```go
// not ready to init
var i int
i = 42
// no way to use := to init float32 (for eg)
var j float32 = 91
// autodetect type
i := 42