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
    <a href="#functions-structs-interfaces">Methods</a>
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
>=| bigger than or equal | 10 >= 10
+| Add | (numbers) 1 + 1 = 2 <br> (strings) "Hello" + " World" = "Hello World" 
-| Subtract | 3 - 2 = 1
*| Multiply | 2 * 2 = 4
/| Divide | 4 / 2 = 2
%| Modulus | 10 % 3 = 1
&&| Logical And | (1 == 1) && ("a" == "a") = true
&#124; &#x7C; | Logical Or | (1 == 1) &#124; &#x7C; ("a" == "b") = true
```

### Conditionals & Loops
```go
if, else , else if
infinite for, for 0, for index_range, while
switch 
```

### Loops
*for* is Go only loop, Below is some example of using *for*
#### For / While / ForEach
```go
package main

import "fmt"

func main() {
    //While loop
    n := 0
    for n < 3 {
        n += 1
        fmt.Println(n)
    }
    
    //Infinite loop
    for {
        fmt.Println("never gonna stop")
    }
    
    // Three component loop
    
    for i := 0; i < 10; i ++ {
        fmt.Println(i)
    }

    // For each range loop
    cardSuits := []string{"Hearts", "Diamonds", "Spades", "Clubs"}
    for idx, suit := range cardSuits {
        fmt.Println(idx, suit)
    }
    
    // Continue
    for i:=0; i < 10; i++ {
        if i%2 == 0 {
            continue
        }
        fmt.Println(i)
    }
    
    // Break
    for i:=0 ; i < 10; i++ {
        if i%2 == 0 {
            break
        }
        fmt.Println("This will not be printed")
    }
    // GOTO
    gotoExample()
}

func gotoExample(){
    fmt.Println("a")
    goto END
    fmt.Println("b")
END: fmt.Println("c")
}

```
#### Switch
```go
package main

import "fmt"

func main() {
    alphaSlice := []string{"a", "b", "c"}
    for _, alpha := range alphaSlice {
        switchExample(alpha)
    }
}
func switchExample(alpha string) {
    switch alpha {
    case "a": fmt.Println("A")
    case "b": fmt.Println("B")
    default:
        fmt.Println("Not A and Not B")
    }
}
```

---

[//]: # ()
## Functions / Methods, Structs & Interfaces
**Functions/Methods**: Declare using keyword `func`. 
- Syntax: `func name(input string)string{}`
<br> 

**Structs**: Declare using `type`, name of struct and keyword `struct` with field/properties.
- Syntax: `type NameOfStruct struct { fieldName string }` 
<br>

**Interface**: Declare using `type`, name of interface and keyword `interface` with method signature.
- Syntax: `type NameOfInterface interface { getValue() string }`
<br>

### Functions / Methods
Below are some examples of functions.
```go
package main

import "fmt"

var pl = fmt.Println

func main() {
    funcWithNoArgument()
    pl("==========================")
    funcWithSingleArgument("Single Argument")
    pl("==========================")
    funcWithMultipleArgument("function", "with mulitple argument")
    pl("==========================")
    s := funcWithSingleArgumentAndResp("Hello")
    pl(s)
    pl("==========================")
    s1, s2 := funcWithSingleArgumentAndMultiResp("function with single argument and multi response")
    pl(s1, s2)
    pl("==========================")
    boolean, number := funcWithMultiTypeResp()
    pl(boolean, number)
    pl("==========================")
}
func funcWithNoArgument(){
    pl("Hello World")
}

func funcWithSingleArgument(arg string) {
    pl(arg)
}

func funcWithMultipleArgument(arg1, arg2 string) {
    pl(arg1,arg2)
}

func funcWithSingleArgumentAndResp(arg string) string {
    pl(arg)
    return "World"
}
func funcWithSingleArgumentAndMultiResp(arg string) (string, string) {
    pl(arg)
    return "Multi", "Response"
}

func funcWithMultiTypeResp() (bool, int) {
    return true, 1
}

```
### Structs
Below is an example of struct.
```go
package main

import "fmt"

type Card struct {
    cardSuit  string
    cardFace  string
}

type deck = []Card

func newDeck() deck {
    cardSuits := []string{"Hearts", "Diamonds", "Spades", "Clubs"}
    cardFace := []string{"Ace", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"}
    cardDeck := deck{}

    for _, suit := range cardSuits {
        for _, face := range cardFace {
            card := Card{cardSuit: suit, cardFace: face}
            cardDeck = append(cardDeck, card)
        }
    }
    return cardDeck
}

// Functions can also benefit from Struct, by putting a receiver,  
//functions can be used like this, card.getCardValue()
func (c Card) getCardValue() {
    fmt.Printf("%s of %s ", c.cardFace, c.cardSuit)
}

func main() {
    cardDeck := newDeck()
    cardDeck[1].getCardValue()
    fmt.Printf("%+v", cardDeck)
}
```
### Interfaces
Below is an example of interface
```go
type Shape interface {
    Area() float64
}
```
### Pointers and Defer
### Channels
### WaitGroup
### Mutex
### Race Conditions
### Deadlock
















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

