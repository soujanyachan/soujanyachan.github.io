
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
	- https://www.callicoder.com/docker-golang-image-container-example/

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

# primitives
- types
	- boolean type
	- numeric types
		- integers
		- floating point
		- complex numbers
	- text types
```go
var n bool = true
var k := 1 == 1 // true
var j := 2 == 1 // false
var l bool // 0 value is false

// int depends on system but at least 32 bits
var n int16 = 42
var n1 uint16 = 42

//(byte)
// bit operator
// & , | , ^ , &^
// <<, >> bitshifts
n := 3.q4
n = 13.7e72
n = 2.1E14
// always float64 by default
// complex type
var n complex64 = 2i
real(n), imag(n)
complex(5,12) // real, imag 5+12i

//text
s := "string"
s[2] // 105 uint8 
b:=[]byte(s) // array of uint8s byte slices

//rune - utf32
r:='a' // single quotes, type alias for int32
var r rune = 'a'
```

# constants
- naming convention
- typed constants
- untyped constants
- enumerated constants
- enumerated expressions

```go
const myConst int = 42
// can't assign computed value
```
- constants can be shadowed, changing type
- implicit conversions when working with constants as compiler directly replaces

- enumerated const
	- `iota` starts at zero
	- the default value of a variable is the zero value of it, so may cause errors
	- so use the first in the enum as the error value / __
	- fixed offset ofr enums can be done

# arrays and slices
- arrays
	- creation
	- builtin functions
	- working with arrays
- slices
	- creation
	- built ins
	- working with slices

```go
grades := [3]int



```