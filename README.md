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
    <a href="#variables-types-constants">Variables</a> •
    <a href="#conditionals-operators">Conditionals</a> •
    <a href="#loops-switchcase">Loops</a> •
    <a href="#functions-structs-interfaces">Methods</a>
</p>

![screenshot](https://cool-thing.gif)

[//]: # ()
## Variables, Data Types, Constants
Containers for storing data values


### Syntax
`keyword` `variableName` `type` = `value`

`variableName` **:=** `value`

> [**Walrus** operator] - The **(var, const)** keyword can be omitted, type will be inferred based on the value

#### Numbers
```go
var (
    uint8, // a.k.a byte
	uint16,
	uint32,
	uint64,
	int8,
	int16,
	int32, // a.k.a rune
	int64, 
	float32,
	float64,
	complex64,
	complex128
)
```
#### Strings, Booleans
```go
package main 
import "fmt"
func main() {
    var s string = "string"
    var b bool
    fmt.Println(s, b)
}
```
#### Collections
Array cannot be resized after declaring its length. <br>
Slice dynamically sized, more flexible.
```go
package main

import "fmt"

func main() {
    var arr = [3]string {"This", "Is", "Array"} 
    var slice = []string {"This", "Is", "Slice"}
    var m = make(map[string]string)
    m["key"] = "value"

    fmt.Printf("%+v, length:%d \n", arr, len(arr))
    fmt.Printf("%v, length:%d \n", slice, len(slice))
    fmt.Println("map: ", m)
}

```
#### Zero values
```go
package main

import "fmt"

func main() {
    var i int //output 0
    var f float32 //output 0
    var b bool //output false
    var s string // output ""
    
    fmt.Printf("%v, %v, %v, %q \n", i, f, b, s)
}


```
#### Constants
Constant declare with `const` keyword <br>
Constant can be character, string, boolean or numeric value. <br>
Cannot be declared using `:=` syntax

```go
package main

import "fmt"

func main()  {
    const A = "Constant String"
    //will give you this message when you run go run main.go
    //cannot assign to A (untyped string constant "Constant String")
    // A = "bc"

    fmt.Println(A)
}
```
---

[//]: # ()
## Conditionals
Arithmetic, assignment, logical/bitwise comparison
### Conditionals
```go
package main
import "fmt"

func main(){
    i := 9
    if i < 5 {
        fmt.Println(i , "is smaller than 5.")
    } else if i < 0 {
        fmt.Println(i , "is negative.")
    } else {
        fmt.Println(i, "is positive.")
    }
}
```
### Operators
> <, >, <=, >=, +, -, *, /
---

[//]: # ()
## Loops
TODO: description
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
TODO: description
### Functions / Methods
Functions/ Methods are created with the following syntax
`func functionName(argument argumentType) returnType {}`
Below are some examples of function.
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
Go’s structs are typed collections of fields. They’re useful for grouping data together to form records.
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

