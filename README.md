<div style="background-image: url(assets/go_background.webp)">
    <h1 align="center" style="background-image: url(assets/go_background.webp)">
      <br>
      <a href=""><img src="assets/go_logo.png" alt="GO Lang" width="200"></a>
      <br>
      Go Cheatsheet
      <br>
    </h1>
</div>
<h4 align="center">Build simple, secure, scalable systems with <a href="https://go.dev" target="_blank">Go</a>.</h4>
<p align="center">
  <a href="">
      <img src="https://img.shields.io/badge/documentation-v1-1EAEDB.svg">
  </a>
  <a href="">
    <img src="https://img.shields.io/badge/language-go-ff69b4.svg?&amp;style=flat">
  </a>
</p>
<p align="center">
    <a href="#Setup">Setup</a> •
    <a href="#types-variables-constants-zeros">Data Types</a> •
    <a href="#operators-conditionals-loops">Control Structures</a> •
    <a href="#functions-structs-interfaces">Methods</a> •
    <a href="#goroutines-waitgroups-channels-mutex">Concurrency</a>
</p>

<details>
    <summary>Table of Contents</summary>
    <ol>
        <li>Chapter</li>
        <ul>
            <li>sub-chapter</li>
        </ul>
    </ol>
</details>

[//]: # (Setup)
## Introduction & Setup
- [Download & Install](https://go.dev/doc/install)
- [Documentation](https://go.dev/doc/)
- [Tips](https://go.dev/doc/effective_go)

### New Project
```bash
go mod init ${company}.${tld}/${projectName}/${moduleName}
```
This will create a `go.mod` file to track your code dependencies
```bash
go get -u ${module}
```
This will install modules into your `go.mod` file and create a `go.sum` file to verify module checksums
```bash
go mod tidy # Will convert modules in go.mod to be use directly Default: #indirect
go mod verify # Will verify module checksums
go list -m all # List all mods
go list -m -versions github.com/gin-gonic/gin # List available versions for a mod
go mod why github.com/gin-gonic/gin # Shows dependency tree
go mod graph # Show module requirement graph
go mod vendor # Downloads modules to local folder (e.g node_modules)
```

### Base Go Project
```go
package main // Base package

// Import required modules
import "fmt" 
// Declare package-scoped variable
var greeting string
// init will run once on start
func init() { 
	name := "User" // Declare function variable
	greeting = "Welcome " + name
}
// Base main.go file should have the main method as an entry point
func main() {
	fmt.Println(greeting)
}
```

---

[//]: # (DataTypes)
## Data Types, Variables, Constants & Zero-Values
Containers for storing data values. Go is a strongly, statically typed language

### Syntax
`keyword` `variableName` `type` = `value`
> [**keyword**] `var` can be reassigned and redeclared.  `const` is fixed

`variableName` **:=** `value`

> [**Walrus operator**] - The **`var` or `const`** keyword can be omitted, type will be inferred based on the value

### Numbers: Integers and Floating Points
Size and range of `Integers` in go is platform dependant.
The default `int` or `uint` can be
***(32 bits or 4 byte)*** in a **<u>32 bit machine</u>** or
***(64 bits or 8 byte)*** in a **<u>64 bit machine</u>**
```go
var (
    // Signed Datatype
    int_ int               // either 32 or 64 bit
    int8_ int8             // -128:127
    int16_ int16           // -32768:32767
    int32_ int32           // -2147483648:2147483647 (alias = rune)
    int64_ int64           // -9223372036854775808:9223372036854775807

    // Unsigned Datatype
    uint_ uint             // either 32 or 64 bit
    uint8_ uint8           // 0:255 (alias = byte)
    uint16_ uint16         // 0:65535
    uint32_ uint32         // 0:4294967295
    uint64_ uint64         // 0:18446744073709551615

    uintptr_ uintptr       // Unsigned integer large enough to store uninterpreted bits of a pointer value
	
    float32_ float32       // 3.40282346638528859811704183484516925440e+38
    float64_ float64       // 1.401298464324817070923729583289916131280e-45 - 
    complex64_ complex64   // represents float32 real and imaginary data
    complex128_ complex128 // represents float64 real and imaginary data
)
```
### Strings, Booleans
```go
var s string = "This is a string"
var b bool = true
```
### Collections
```go
var (
    // Arrays are fixed length collection of elements of the same type
    // ByValue
    array           = [3]int{1, 2, 3}       // Fixed-size
    ellipsesArray   = [...]int{1, 2, 3, 4}  // Compiler will identify length of array
    kvpArray        = [3]string{1: " Two"}  // Can declare using 0-index
    determineOnInit = []int{1, 2, 3}        // if size is not given, (idx + 1) becomes length

    // Slices are abstractions over Arrays
    // ByReference
    slice          []int                    // Declare without specifying size and values. (== nil)
    sliceFromArray = array[:len(array)]     // Slice made from an array
    shorthandSlice = array[:]               // Shorthand method of above
    pointerSlice   = &array                 // Another way of achieving the above
    MaxSlice       = slice[:cap(slice)]     // Expand to maximum size
    makeSlice      = make([]int, 3, 3)      // Make a slice of length 3 and capacity 3

    map_ = make(map[string]string)          // Declare a map of key: string, value: string pairs
    // new() allocates memory but is not initialized, zeroed storage
    // make() allocates memory and initialize, non-zeroed storage
)
```
### Zero values
Some Data Types have default values
```go
var i int       // == 0
var f float32   // == 0
var b bool      // == false
var s string    // == ""
var x []int     // == nil
```
### Pointers and Values
A pointer is a variable that stores the memory address of another variable.
Pointers are used to pass variables by reference and manipulate data structures directly in memory.

`&` pointer to memory address (reference).
<br>
`*` resolved value from memory address pointer (value)
```go
// Declare variable x
var x int = 5
// Declare a pointer of type *int which points to the address of x using the '&' symbol
var xPtr *int = &x

// To access the value
fmt.Println("Value of x:", x)       // Output 5
fmt.Println("Value of xPtr:", *ptr) // Output: 5
```
---

[//]: # (Control Structures)
## Control Structures
Arithmetic, assignment, logical/bitwise comparison
### Operators
Symbol | Description | Example
:---:|---|---
<| Less than | 1 &nbsp; < &nbsp; 9
\>| Bigger than | 9 &nbsp; > &nbsp; 1
<=| less than or equal | 10 <= 10
\>=| bigger than or equal | 10 >= 10
+| Add | (numbers) 1 + 1 = 2 <br> (strings) "Hello" + " World" = "Hello World" 
-| Subtract | 3 - 2 = 1
*| Multiply | 2 * 2 = 4
/| Divide | 4 / 2 = 2
%| Modulus | 10 % 3 = 1
&&| Logical And | (1 == 1) && ("a" == "a") = true
&#124; &#x7C; | Logical Or | (1 == 1) &#124; &#x7C; ("a" == "b") = true
### Conditionals & Loops
#### if / else if / else
```go
import "math/rand"
...
// Give the random a seed number
rand.Seed(time.Now().UnixNano())
// Generate a random number between 1 - 6
var number int = (rand.Intn(6) + 1)

func report(num int) {
	fmt.Println("number is:", num)
}

// if, else if, else example
if number >= 1 && number < 3 {
    report(number) // number is 1 or 2
} else if number == 3 || number <= 4 {
    report(number) // number is 3 or 4
} else {
    report(number) // number is 5 or 6
}
```
#### For Loops
Go only has `for` loops, therefore concepts such as `while` and `forEach` are done differently
```go
// An infinite loop
for {
    fmt.Println("Will run forever")
}

...

// Goto declaration
greeting:
    fmt.Println("You got the Joker!")
// declare a slice of card suits
var cardSuits = []string{"Clubs", "Diamonds", "Hearts", "Spades", "Joker"}
// For index range
for idx, suit := range cardSuits {
    if suit == "Joker" {
        // goto: will exit the loop and go to the defined greeting method
        goto greeting
    }
    fmt.Printf("The order is: %v, suit: %v", idx+1, day)
}

...

// While Loop
for i := 0; i < 3 {
    i += 1
    fmt.Println(i)
    // this will run 3 iterations
}

...

// 3 Component Loop with Continue and Break
for i := 0; i < 3; i++ {
	mod := i%2
	if mod == 0 {
	    continue // will stop current iteration and increment i
    }
	if mod == 1 {
	    break // will exit the loop
    }
}
```
#### Switch
```go
// Give the random a seed number
rand.Seed(time.Now().UnixNano())
// Generate a random number between 1 - 7 on purpose
var diceRoll int = (rand.Intn(7) + 1)
// This demonstrates the multiple ways to group cases
switch diceRoll {
    // single case match
    case 1:
        fmt.Println("You got the lowest number!")
    // multiple case matching
    case 2, 3, 4: fmt.Println("You got a low number!")
	// fallthrough will also run the methods in the case below it
    case 5:
        fallthrough
    case 6:
        fmt.Println("You got a high number!")
    default:
        fmt.Println("This is not part of the dice!")
}
```

---

[//]: # (Functions&Methods)
## Functions / Methods, Structs & Interfaces
### Syntax
func `functionName`(`...argumentsWithType`) (`...returnTypes`) {...}
> functions can have 0..* arguments.
> They can also return 0..* values

type `typeName` interface {...}
> `interfaces` are abstract types that define a set of method signatures
> All methods declared in an interface must be implemented

type `typeName` struct {...}
> `structs` are custom concrete types
> Types that implement all the methods is considered to implement the interface
```go
// Define a shape interface
type Shape interface {
    Area() float64
}
// Define a Circle struct which is a type of shape
type Circle struct {
    radius float64
}
// Implement the methods from the Shape interface
func (c Circle) Area() float64 {
    return math.Pi * c.radius * c.redius
}
// Function that takes in an argument of Shape
func PrintArea(s Shape) {
    fmt.Println("Area:", s.Area())
}
// Initialize a Circle type and call the PrintArea function
func main() {
    c := Circle{radius: 5}
    PrintArea(c)
}
```
A `struct` can also implement multiple interfaces
```go
// Define an interface for Daytime
type Daytime interface {
    SunPosition()
    GetTemperature()
}
// Define an interface for Nighttime
type Nightime interface {
    MoonPhase()
    GetTemperature()
}
// Define an Environment struct that can be a Day or Night type
type Environment struct {
    sunPosition string
    moonPhase string
    temperature float64
}
// Implement all the methods in the interface
func (e Environment) SunPosition() string {
    fmt.Printf("The Sun is at %v\n", e.sunPosition)
    return e.sunPosition
}
func (e Environment) MoonPhase() string {
    fmt.Printf("The Moon is %V\n", e.moonPhase)
    return e.moonPhase
}
func (e Environment) GetTemperature() float64 {
	fmt.Printf("The temperature now is: %v\n", e.temperature)
    return e.temperature
}
func main() {
    environment := Environment{
        sunPosition: "Midday",
        moonPosition: nil,
        temperature: 30.5
    }
	// The Environment struct can now be a combination of either interface
    var daytime Daytime = environment
    var nighttime Nighttime = environment
}
```
An example of a function that takes in multiple argument types and returns multiple types
```go
// This is an empty interface. It does not contain any method signature in its declaration
var interface_ interface{}
// the 3-dots ligature is called a variadic function
func Println(i ...interface{}) (i int, err error) {...}
// An example of the above. the '_' underscore is a blank identifier. to indicate an unused variable
int_, _ := fmt.Println("a-string", 69, []float64{1.2, 3.4})
```

---

[//]: # (Concurrency)
## Concurrency & goroutines
### Defer
in Go, a goroutine is a lightweight thread of execution that are used to perform concurrent operations
to create a new goroutine, we use the 'go' keyword
```go
func add(a, b int, c chan int) {
	sum := a + b
	c <- sum
}

func main() {
	c := make(chan int)
	go add(1, 2, c)
	sum := <-c
	fmt.Println("Sum:", sum)
}
```
```go
func goroutinesMutexExample() {
	wait := &sync.WaitGroup{}
	mut := &sync.RWMutex{}
	endpoints := []string{
		"https://google.com",
		"https://github.com",
		"https://fb.com",
		"https://twitter.com",
		"https://go.dev",
	}

	signals := make([]string, 0)

	getStatus := func(endpoint string) {
		defer wait.Done()
		res, err := http.Get(endpoint)
		if err != nil {
			fmt.Println("[Error] -", endpoint)
		} else {
			mut.Lock()
			signals = append(signals, endpoint)
			mut.Unlock()
			fmt.Printf("%v for %v\n", res.StatusCode, endpoint)
		}
	}

	for _, endpoint := range endpoints {
		wait.Add(1)
		go getStatus(endpoint)
	}
	wait.Wait()
	fmt.Println(signals)

	/*
		[_Mutex_] - Mutual Exclusion Lock
			- Zero value for a Mutes is unlocked
			- Must not be copied after run
	*/
}
```
### Channels
### WaitGroup
### Mutex
### Race Conditions
### Deadlock

## File, IO, Http
















[//]: # (Use this template)
## Main Topic
description
### Sub-Header (Items)
#### thing (Points for each item)

> **Info**
> description, [link](https://link.to) `go-command`

---

> [Credit-Link-Here](https://link.me) &nbsp;&middot;&nbsp;
> [Some-Other-Thing](https://link.me)

