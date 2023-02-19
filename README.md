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
    <a href="#goroutines-waitgroups-channels-mutex">Concurrency</a> •
    <a href="#file-io-http">Others</a>
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
in Go, a `goroutine` is a lightweight thread of execution that are used to perform concurrent operations
to create a new goroutine, we use the `go` keyword.
`WaitGroups` and `Channels` are synchronization primitives that can be used to coordinate the execution of concurrent code

### WaitGroups
`WaitGroups` are best used when you want to wait for a specific set of `goroutines` to complete before continuing with your program.
It uses a counter that can be **incremented** and **decremented** by using the `Add()` and `Done()` methods.
When the count reaches zero, the `Wait()` method unblocks the calling `goroutine`
```go
// Initialize the WaitGroup, RWMutex, list of tasks and a slice to hold the results
wait := &sync.WaitGroup{}
mut := &sync.RWMutex{}
// Initialize a list of tasks
tasks := []string{ "task_1", "task_2", "task_3", }
results := make([]string, 0)

// Define a function to handle the response
getResult := func(task string) {
    // wait.Done() -> will decrement the WaitGroup counter
    // the `defer` keyword will delay the execution until the end of the function
    defer wait.Done()
    // Perform the concurrent task 
    result := concurrentTask(task)
    // Perform a Read Write lock  
    mut.Lock()
    results = append(results, result)
    // Release the Lock after write is done
    mut.Unlock()
}
// Loop through the tasks and mark them as `goroutines`
// increment the WaitGroup counter
for _, task := range tasks {
    wait.Add(1)
    go getResult(task)
}
wait.Wait()
fmt.Printf("Results: %v\n", results)

/*
    Mutex = Mutual Exclusion Lock
      - Zero value for a Mutes is unlocked
      - Must not be copied after run
*/
```
### Channels
`Channels` allow for communication and synchronization between `goroutines`.
It is used to pass data between `goroutines` and to signal events. It can also be buffered, meaning they can store a certain number of messages before blocking the sender. 
`Channels` are best used when you want to coordinate the flow of data and events between multiple goroutines 
```go
func add(a, b int, c chan int) {
	sum := a + b
	// <- arrow on right-hand-side of channel is to set the value
	c <- sum
}

func main() {
	c := make(chan int)
	// goroutine to do simple addition, passing in the channel
	go add(1, 2, c)
	// <- arrow on left-hand-side of channel is to get the value
	sum := <-c
	fmt.Println("Sum:", sum) // Output: 3
}
```
### Using `WaitGroups` and `Channels` together
Two `goroutines` are created, therefore we add 2 to the `WaitGroup`.
The first function will wait until the channel recieves a value before completing
```go
// Waitgroup
wait := &sync.WaitGroup{}
// Initialize Channel with buffer
myChannel := make(chan int, 2)
// Add 2 count to WaitGroup because there are 2 `go` goroutines called below
wait.Add(2)
// [Receive Only] <- arrow on left-hand-side of function argument
go func(ch <-chan int, wg *sync.WaitGroup) {
    val, isOpen := <-myChannel
    fmt.Println("Channel isOpen: %v, Value: %v \n", isOpen, val)
    wg.Done()
}(myChannel, wait)

// [Send Only] <- arrow on right-hand-side of function argument
go func(ch chan<- int, wg *sync.WaitGroup) {
    myChannel <- 5
    close(myChannel)
    wg.Done()
}(myChannel, wait)

wait.Wait()
```
#### Race Conditions
Race conditions happen when two goroutines are accessing the same variable concurrently.
- **Shared Data** : Multiple goroutines sharing the same data without any `lock` or `unlock` will result in data race conditions. <br>
- **Critical Sections** : Critical sections are block of code where goroutine is attempting to write a variable. Using `lock` and `unlock` would ensures the critical section to be ***atomic***.


#### Deadlock
Deadlocks happen when group of goroutines are waiting for each other but not able to proceed. <br> Go is able to detect when program as a whole freezes but not when subset of goroutines are stuck.

A goroutine can get stuck
- either because it’s waiting for a **channel** or
- because it is waiting for one of the **locks** in the sync package.

Common reasons are that
- no other goroutine has access to the channel or the lock,
- a group of goroutines are waiting for each other and none of them is able to proceed.

---

## Others
### File, IO
#### File
Reading and Writing of file can be done with the help of `os` package.

```go
func (d deck) saveToFile(filename string) error {
	return os.WriteFile(filename, []byte(d.toString()), 0666)
}

func newDeckFromFile(filename string) deck {
bs, err := os.ReadFile(filename)
if err != nil {
    fmt.Println("ERROR: ", err)
    os.Exit(1)
    }
var d deck
    fmt.Println(bs)
}

```
#### IO
**IO** package allow the program to read and capture the information to a variable. Below is an example of how IO can be used.
```go
package main

import (
	"bytes"
	"fmt"
	"io"
	"os"
)

// Your function
func foo(w *io.PipeWriter) {
	defer w.Close()
	// Write a message to pipe writer
	fmt.Fprintln(w, "Hello Medium")
}

func main() {
	// Create a pipe
	pr, pw := io.Pipe()

	// Pass writer to function
	go foo(pw)

	// Variable to get standard output of function
	var b bytes.Buffer

	// Create a multi writer that is a combination of
	// os.Stdout and our variable byte buffer
	mw := io.MultiWriter(os.Stdout, &b)
	// Copies reader content to standard output
	_, err := io.Copy(mw, pr)

	if err != nil {
		panic(err)
	}

	// Optional: verify data
	fmt.Println(b.String())
}
```



### Http with Gin-Gonic
#### Http
In Go, `Http` package can be used to make GET, POST. <br>
**GET**
```go
resp, err := http.Get("http://google.com")
if err != nil {
    fmt.Println(err)
}
defer resp.Body.Close()
```
**POST**
```go
package main

import (
	"bytes"
	"fmt"
	"io/ioutil"
	"net/http"
)

func main() {
	httpposturl := "https://example.com/api/users"
	fmt.Println("HTTP JSON POST URL:", httpposturl)

	var jsonData = []byte(`{
		"name": "John",
		"job": "Developer"
	}`)
	request, error := http.NewRequest("POST", httpposturl, bytes.NewBuffer(jsonData))
	request.Header.Set("Content-Type", "application/json; charset=UTF-8")

	client := &http.Client{}
	response, error := client.Do(request)
	if error != nil {
		panic(error)
	}
	defer response.Body.Close()

	fmt.Println("response Status:", response.Status)
	fmt.Println("response Headers:", response.Header)
	body, _ := ioutil.ReadAll(response.Body)
	fmt.Println("response Body:", string(body))

}
```












> [Credit-Link-Here](https://link.me) &nbsp;&middot;&nbsp;
> [Some-Other-Thing](https://link.me)