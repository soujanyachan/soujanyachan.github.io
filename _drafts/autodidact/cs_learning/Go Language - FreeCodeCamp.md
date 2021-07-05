
# golang freecodecamp
[[golang]]
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

// global variables
// have to use full declaration
var i int = 91

// block of var to define together
var (
	actor string = "Sou"
	season int 11
)```

- can't declare the same variable multiple times
- innermost scope takes precedence -> **shadowing**
- variables always have to be used

visibility / scope
- lowercase and package - scoped to package
- uppercase -> globally outside world
- block scope

rules for variable names
- length of name proportional to the lifetime
- acronyms all uppercase

type casting variables
```go
var i int = 42
var j float32
j = float32(i)
```

reverse is not allowed as you will lose info

string is an alias to a stream of bytes
use strconv to convert strings to other data