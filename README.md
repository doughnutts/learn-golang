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
var String string
var Boolean bool
```
#### Collections
```go
var Array [69]string
var Slice []string
var Map map[string]string{}
```

---

[//]: # ()
## Conditionals
Arithmetic, assignment, logical/bitwise comparison
### Conditionals
> if/else/else if
### Operators
> <, >, <=, >=, +, -, *, /
---

[//]: # ()
## Loops
TODO: description
#### For / While / ForEach
```go
for {...infinite loop...}
for i := 0; i < n; i++ {...}
for idx, movie := range movies {...}
// put examples: continue, break, goto
```
#### Switch
```go
switch () {
    case "x": doSomething()
	default: doSomethingElse()
}
```

---

[//]: # ()
## Fucntions / Methods, Structs & Interfaces
TODO: description
### Functions / Methods
### Structs
### Interfaces
















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

