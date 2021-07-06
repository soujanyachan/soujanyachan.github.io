
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

## variables
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

## primitives
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

## constants
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

## arrays and slices
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

## maps and structs
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

## if and switch statements
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
break is implied, but can also be explicitly said 
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
	fmt.Println("another type")
}
```

## looping
for statement
- simple loops
- exiting early
- looping through collection

```go
for i:=0; i< 5; i++ {
	fmt.Println(i)
}
// go has no comma op to init two in the same loop but can use
// go's ability to init multiple
for i,j:=0,0;i<5;i,j=i+1,j+2{
	fmt.Println(i,j)
}
// increment is not an expression so inside statement cannot
// can manip i inside the loop
for {
	fmt.Println(i)
	i++
	if i==5 {
		break
	}
}
// can also use continue
// labels - (almost like a goto)
s:= []int{1,2,3}
for k,v:=range s {
	fmt.Println(k,v)
}
```


## defer panic and recover
defer functions are called in LIFO order
after fn is done but before it returns
associate the opening and closing of a resource
check twice if open in a loop

defer variables take the value at the time the function is called and not at execution time

panic -> throwing a fatal error, program cannot continue at all
panics after it finishes the deferred statements
recover ->
- catching panics, can either continue panic or recover for the higher functions in the call stack
- only useful in deferred functions

## pointers

- creating pointers 
- dereferencing pointers
- new function
- nil
- internal pointers

```go
var a int = 42
var b *int = &a
fmt.Println(a,b) // value, addr
fmt.Println(&a,b) // addr addr
fmt.Println(a,*b) // value, value

//ptr arithmetic
// no pointer arithmetic in go for simplicity

// dont need to have any underlying data
type myStruct struct {
	foo int
}

var ms *myStruct
ms = &myStruct{foo: 42}
fmt.Println(ms) // &{42}

ms = new(myStruct) // zero values
(*ms).foo = 43 // deref operator has lower precedence that the dot operator so brackets are required
ms.foo // syntactic sugar for (*ms).foo

// internal rep of slice contains pointer
// similarly maps contain pointers
```
a pointer that you dont init will be holding the value `nil`

## functions
- syntax
- params
- returns values
- anonymous fns
- functions as types
- methods

```go
func main() {
	fmt.Println("hello playground")
}

func sayMessage(msg string, idx int) {
	fmt.Println(msg, idx)
}

func sayGreeting(msg, name string) {
	fmt.Println(msg, name)
}

// pass by value and reference
sayGreetingPtr(&greeting, &name);
func sayGreetingPtr(msg, name *string) {
	fmt.Println(msg, name)
}

//variadic params - has to be at end and only one
func sum(msg string, values ...int) {
	fmt.Println(values)
	// values acts like a slice
}

// return values
// return a local variable as a pointer, return &result
// golang autopromotes the variables to heap memory from the local stack
// named return values (result int) -> that value is implicitly returned -> slightly difficult to read
// return error obj fmt.Errorf("cannot") // value, nil


// anon fn
func() {
	fmt.Println("ejkn")
}() // IIFE
// for anon fns pass the input params by value to prevent issues when running async code

f:=func() {
	fmt.Println("sdf")
}
f()

// method (fn inside known context)
func (g greeter) greet(){
	// copy of g greeter obj by default, you can pass pointer if reqd
	fmt.Println(g.greeting, g.name)
} 
```

## interfaces
- how make
- composing
- type conv
	- empty
	- type switches
- implementing value vs ptr
- best practices

```go
func main() {
	var w Writer = ConsoleWriter{}
	w.Write([]byte("Hello go"))
}

type Writer interface {
	Write([]byte) (int, error)
}

type ConsoleWriter struct {}

func (cw ConsoleWriter) Write(data []byte) (int, error) {
	n, err := fmt.Println(string(data))
	return n, err
}
// advantage of this is that we get polymorphic behaviour
// implicit implementation
// single method interface should be name by the method + 'er'
// composing interface
type Writer interface {
	Write([]byte) (int, error)
}

type Closer interface {
	Close() error
}

type WriterCloser interface {
	Writer
	Closer
}

//interface conversion 
// empty interface -> then do conversion
// write method has pinter receiver
// methodset associated with the type, but for interfaces 

```

An interface is two things: it is a set of methods, but it is also a type.

Since there is no `implements` keyword, all types implement at least zero methods, and satisfying an interface is done automatically, _all types satisfy the empty interface_. That means that if you write a function that takes an `interface{}` value as a parameter, you can supply that function with any value.

An interface value is constructed of two words of data; one word is used to point to a method table for the value’s underlying type, and the other word is used to point to the actual data being held by that value. [^1]

To implement an interface in Go, we just need to implement all the methods in the interface.[^2]

Go's interfaces let you use duck typing (In duck typing, an object's suitability is determined by the presence of certain methods and properties, rather than the type of the object itself.[^3]) like you would in a purely dynamic language like Python but still have the compiler catch obvious mistakes like passing an `int` where an object with a `Read` method was expected, or like calling the `Read` method with the wrong number of arguments.[^4]

A golang interface is a lens through which you can view different type definitions. If the type has the methods in the interface it implicitly implements the interface. A single type can "implement" many such interfaces.[^5]

interfaces decouple different types from each other. The interface only describes the expected behaviour. All types are concrete except interface.
bigger the interface, weaker the abstraction.
![[Screenshot 2021-07-06 at 20.06.38.png]]
[^6]


[^1]: https://jordanorelli.com/post/32665860244/how-to-use-interfaces-in-go
[^2]: https://gobyexample.com/interfaces
[^3]: https://en.wikipedia.org/wiki/Duck_typing
[^4]: https://research.swtch.com/interfaces
[^5]: https://www.youtube.com/watch?v=lh_Uv2imp14 - Golang Tutorial #22 - Interfaces - Tech with Tim
[^6]: https://www.youtube.com/watch?v=qJKQZKGZgf0 - Learn Go Programming - interfaces