
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
grades := [...]int{9,10,1}
var students[3]string
students[0]="List"
len(students)

```

array copying is a deep copy
if you want shallow copy 
```go
b := &a
```

slices - copies are shallow copies
```go
a := []int{1,2,3,4,5,6,7,8,9,10}
b := a[:] // all elements
c := a[3:] // index 3 to end
d := a[:6] // index 0 to 6(not inclusive)
e := a[3:6]
```

first num is inclusive and second is exclusive
slicing ops can have as input array or slice

```go
a := make([]int, 3)
// capacity planning for the array
b := make([]int, 100)
a = append(a, 1)
a = append(a, 1,2,3,4)
// uses the doubling method of increasing space in the slice
// spread operator
a = append(a, []int{1,23,4}...)
```

# maps and structs
- maps
	- what they are
	- creation
	- manip
- structs
	- what
	- creation
	- naming convention
	- embedding
	- tags

```go
pops := map[string]int{
	"c": 123,
	"d": 124
}

pops := make(map[string]int)
pops["g"] = 120
// return order of map is not guaranteed
delete(pops, "g");
pop, ok := pops["g"] // value, status code
// map is also shallow copied
```

structs
```go
// pascal and camel casing in the struct dont use underscores
type Doctor struct {
	Number int
	actorName string
	companions []string
}

aDoctor := Doctor{
	Number: 10,
	actorName: "David Tennant",
	companions: []string {
		"Amy Pond",
		"Donna Noble"
	}
}
// not as good, put the fields also!!
aDoctor := Doctor{
	10,
	"David Tennant",
	[]string {
		"Amy Pond",
		"Donna Noble"
	}
}
aDoctor.companions[1]

//anon struct, initialiser - usually very shortlived
// struct is deep copy
aDoctor:= struct{name string}{name: "David Tennant"}
anotherDoc := aDoctor
anotherDoc.name = "TomBaker"
aDocter // {David Tennat}
anotherDoc // {TomBaker}

//shallow copy we can use
anotherDoc:= &aDoctor
```

embedding one struct in another
inheritance vs composition
not a traditional inheritance relationship ie bird is an animal
more like composition where bird has an animal

tags
```go
type Animal struct {
	Name string `required max:"100"`
}

t:=reflect.TypeOf(Animal{})
field,_:= t.FieldByName("Name")
field.Tag // required max: "100"
```

# if and switch statements
- if
	- operators
	- if else, if else if
- switch
	- simple
	- multiple tests
	- faling through
	- type switches

```go
// always use curly
if false {
	fmt.Println("dkjnsdkj")
}

if pop, ok := pops["f"]; ok {
	fmt.Println(pop)
}
// comparison
< , >, ==
>=, <=, !=
//shortcircuit
lazy eval of the tests
//logical ops
||, &&, !(not)
```

switch
falling through is not there, but multiple case checks in single block
tagless syntax for case, full comparisons, they are allowed to overlap, and first returns
break is implied
can use the keyword fallthrough, logicless

type switch
```go
var i interface{} = 1
switch i.(type) {
case int:
	fmt.Println("int")
case string:
	fmt.Println("string")
default:
	fmt.Println()
}
```