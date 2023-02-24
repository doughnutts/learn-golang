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
    <a href="#introduction--setup">Setup</a> •
    <a href="#data-types-variables-constants--zero-values">Data Types</a> •
    <a href="#control-structures">Control Structures</a> •
    <a href="#functions--methods-structs--interfaces">Methods</a> •
    <a href="#concurrency--goroutines">Concurrency</a> •
    <a href="#others">Others</a>
</p>

<details>
    <summary>Table of Contents</summary>
    <ol>
        <li>
            <a href="#introduction--setup">Introduction & Setup</a>
        <ul>
            <li><a href="#new-project">New Project</a></li>
            <li><a href="#base-go-project">Base Go Project</a></li>
        </ul>
        </li>
        <li>
            <a href="#data-types-variables-constants--zero-values">Data Types, Variables, Constants & Zero-Values</a>
            <ul>
                <li><a href="#syntax">Syntax</a></li>
                <li><a href="#numbers-integers--floating-points">Numbers: Integers & Floating Points</a></li>
                <li><a href="#strings--booleans">Strings & Booleans</a></li>
                <li><a href="#collections">Collections</a></li>
                <li><a href="#zero-values">Zero Values</a></li>
                <li><a href="#pointers--values">Pointers & Values</a></li>
            </ul>
        </li>
        <li>
            <a href="#control-structures">Control Structures</a>
            <ul>
                <li>
                    <a href="#conditionals--loops">Conditionals & Loops</a>
                    <ul>
                        <li><a href="#if--else-if--else">if / else if / else</a></li>
                        <li><a href="#for-loops">For Loops</a></li>
                        <li><a href="#switch">Switch</a></li>
                    </ul>
                </li>
            </ul>
        </li>
        <li>
            <a href="#functions--methods-structs--interfaces">Functions / Methods, Structs & Interfaces</a>
            <ul>
                <li><a href="#syntax-1">Syntax</a></li>
            </ul>
        </li>
        <li>
            <a href="#concurrency--goroutines">Concurrency & goroutines</a>
            <ul>
                <li><a href="#waitgroups">WaitGroups</a></li>
                <li><a href="#channels">Channels</a></li>
                <li><a href="#using-waitgroups-and-channels-together">Using WaitGroups and Channels together</a></li>
                <li><a href="#race-conditions">Race Conditions</a></li>
                <li><a href="#desklock">Deadlock</a></li>
            </ul>
        </li>
        <li>
            <a href="#others">Others</a>
            <ul>
                <li>
                    <a href="#file-io">File, IO</a>
                    <ul>
                        <li><a href="#file-operations">File Operations</a></li>
                        <li><a href="#io">IO</a></li>
                    </ul>
                </li>
                <li><a href="#http-server-with-gin-gonic">Http Server with Gin-Gonic</a></li>
                <li><a href="#http-client">Http Client</a></li>
                <li><a href="#parsing-json-data">Parsing JSON Data</a></li>
            </ul>
        </li>
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
This will create a `go.mod` file to track and manage your code dependencies
> **Note** It is not mandatory to run this. `Modules` was introduced in Go `1.11` onwards.
> Read more about the changes [here](https://devopscon.io/blog/go-1-11-new-modules/)
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
### Strings & Booleans
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
### Zero Values
Some Data Types have default values
```go
var i int       // == 0
var f float32   // == 0
var b bool      // == false
var s string    // == ""
var x []int     // == nil
```
### Pointers & Values
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
There are instances where additional information are needed from files, this can be achieved using the `os` package.
#### File Operations
```go
func WriteToFile() {
    // Create the file using the `os` mod. Remember to close the file
    file, err := os.Create("./greeting.txt")
    content := "Hello, World!"
    defer file.Close()
    // Handle error if exists
    if err != nil {...}
    // Write to file
    length, err := io.WriteString(file, content)
    // Can also use below method for writing to file
    os.WriteFile(file.Name(), []byte(content), 0666)
    if err != nil {...}
    fmt.Printf("length of file is: %v\n", length)	
}

func ReadFromFile(filename string) {
    databyte, err := os.ReadFile(filename)
    // Handle error if exists
    if err != nil {...}
    fmt.Println("File Contents: ", string(databyte))
}
```
#### IO
One of a way to retrieve inputs from CLI is shown below.
```go
    // Option 1: Using fmt.Scan to variable address
    var firstName string
    fmt.Println("Enter your first name:")
    fmt.Scan(&firstName)

    // Option 2" Using a buffered reader
	reader := bufio.NewReader(os.Stdin)
	fmt.Print("Enter Weight:")
	weightInput, err := reader.ReadString('\n')
	if err != nil {...}
    age, err := strc.ParseFloat(str.TrimSpace(weightInput), 64)
	
	fmt.Printf("Name: %v, Age: %v \n", firstName, age)
```
#### Http Server with Gin-Gonic
Gin is an HTTP Web Framework written in Go. 
Below is an example of using Gin, for more examples, [click here.]("https://github.com/gin-gonic/examples") 
```go
import "github.com/gin-gonic/gin"
...
// Declare a new instance of gin
router := gin.Default()
// Add any middleware functions
router.Use(
	CustomHandler()
    gin.Recovery(),
    // RateLimiting
    // ErrorHandling
    // CORS
    // SecurityConfigs
)
// Define your own middleware
func CustomHandler() gin.HandlerFunc {
    return func(c *gin.Context) {...}
}

// Add a handler if API endpoint does not exist
router.NoRoute(func(c *gin.Context) {
    c.AbortWithError(http.StatusNotFound, errors.New("PAGE NOT FOUND"))
})

// Grouping helps in reducing boilerplate code by gathering all endpoints that have similar paths
apiGroup := router.Group("/api")
// This will resolve to http://localhost:8080/api/{id}
apiGroup.GET("/:id", func(c *gin.Context) {
	// Get param value from URI 
	id := c.Params.ByName("id")
	// Get query parameters ?age=69 
	other := c.Query("age")
    result, err := backendCall(id)
    if err != nil {
		// Will return HTTP400 with the error
        c.AbortWithError(http.StatusBadRequest, err)
        return
    }
	// Will return HTTP200 with the message
    c.JSON(http.StatusOK, gin.H{"message": result})
    return
})
// Other HTTP types
router.POST("/post", handlePostCall)
router.PUT("/put/:id", handlePutCall)
router.DELETE("/delete/:id", handleDeleteCall)
router.PATCH("/patch/:id", handlePatchCall)
router.HEAD("/", handleHeadCall)
router.OPTIONS("/", handleOptionsCall)

// Start the router. If argument not given, it defaults to :3000
router.Run(":8080")
```
#### Http Client
```go
import (
    "net/http"
    "net/url"	
)

const myurl = "https://httpbin.org/get?hello=world"
// Convenient library to parse URIs
result, err := url.Parse(myurl)
if err != nill {...}
fmt.Printf("Scheme: %v, Host: %v, Path: %v, Port: %v, RawQuery: %v, Query: %v\n",
    result.Scheme, result.Host, result.Path, result.Port(), result.RawQuery, result.Query())

// Http GET call. defer to close the response body read buffer
response, err := http.Get(myurl)
if err != nil {...}
defer response.Body.Close()

var responseString str.Builder
content, _ := io.ReadAll(response.Body)
fmt.Printf("Data: %v\n", responseString.String())
```
#### Parsing JSON Data
```go
import "encoding/json"

// the right-hand-side tags define how the struct should be displayed in JSON
// `omitempty` = hide attribute from output if empty
// `-` = hide from output
type course struct {
    Name     string   `json:"courseName"`
    Price    int      `json:"price"`
    Tags     []string `json:"tags,omitempty"`
    Password string   `json:"-"`
}

func ParseJsonFromStruct() {
    myCourse := []course{
    {"tess", 123, []string{"1", "2", "3"}, "qwe"},
    {"ting", 456, nil, "asd"},
    }
    // Marshal the struct into a JSON object with Indentation
    finalJson, err := json.MarshalIndent(myCourse, "", "\t")
    if err != nil {...}
    fmt.Printf("%s\n", finalJson)
}

func ParseJsonFromWeb() {
    jsonDataFromWeb := []byte(`
    {
        "courseName": "test",
        "price": 123,
        "tags": ["1", "2", "3"]
    }
    `)
    var myCourse course
    // Helper function to check validity of JSON 
    if json.Valid(jsonDataFromWeb) {
        // Unmarshal data to pointer address of course 
        json.Unmarshal(jsonDataFromWeb, &myCourse)
        fmt.Printf("%#v\n", myCourse)
    } else {
        fmt.Println("JSON not valid")
    }

	// Can also Unmarshal into a Key Value Map
    var onlineData map[string]interface{}
    json.Unmarshal(jsonDataFromWeb, &onlineData)
    fmt.Printf("%#v\n", onlineData)
    fmt.Printf("%v\n", onlineData)
}
```

...

[//]: # (Frameworks)
## Frameworks
### microservices
### ORM
ORM  `Object-relational mapping` allows user to query and manipulate data from a database using an object-oriented paradigm.
[GORM](https://gorm.io/docs/index.html) is an ORM Library that is written for GO which aims to be developer friendly. 

A simple demo using `GORM` is provided below.
```go
package main
import (
    "gorm.io/gorm"
    "gorm.io/driver/postgres"
)

type Product struct {
    gorm.Model
    Code string
    Price uint
}

func main() {
    var prodList = []Product{{Code: "A3", Price: 10}, {Code: "A3", Price: 15}, {Code: "A4", Price: 17}}
    
    dsn := "host=localhost user=postgres password=postgres dbname=shops port=9920 sslmode=disable TimeZone=Asia/Shanghai"
    db, err := gorm.Open(postgres.Open(dsn), &gorm.Config{})
    
    if err != nil {
        panic("Connection to DB failed")
    }
    
    db.Create(&Product{Code: "A1", Price: 10}) //Pass pointer of data to Create 
    db.Model(&Product{}).Create(map[string]interface{} {"Code":"A5", "Price":29}) //Create from map
    db.CreateInBatches(&prodList)
    
    
    var p Product
    db.First(&p, 1) // Find product with primary key
    db.First(&p, "code=?", "A1") // Find product with code A1
    
    db.Model(&p).Update("Price", 15) // Update product price to 15
    db.Model(&p).Updates(Product{Price:20, Code: "A2"}) // Update multiple fields
    
    db.Delete(&p, 1) // Delete product
    
}
```

Create With Association
```go
type Product struct {
    gorm.Model
    code string
    price uint
    supplier Supplier
}

type Supplier struct {
    gorm.Model
    name string 
    contactNo string
    
}

// Insert into `products`, `suppliers` respectively.
db.Create(&Product{code: "A1", price: 10, supplier: Supplier{Name: "BiscultGem.Co", ContactNo: "11111111"}})


```
Samples of Retrieval. For more, [click here.](https://gorm.io/docs/query.html)

```go
// Select one record, no specific order
db.Take(&p)

// Get Count of records found
result := db.First(&p)
result.RowsAffected // Count of records found
result.Error // Errors or nil

// Using db.model, SELECT * FROM products ORDER BY products.Code LIMIT 1
result := map[string]interface{}{}
db.Model(&Product{}).first(&result)

//Retrieve all

result := db.Find(&p)
p.RowsAffected
p.Error

// Conditions
//Find first matching record
db.Where("code = ?", "A1").First(&p)

//Find all matching records
db.Where("code <> ?", "A1").Find(&p)

//Like
db.Where("code LIKE ?", "%A%").Find(&p)

//AND
db.Where("code = ? AND price = ?", "A1", 10).Find(&p)

//Struct
db.Where(&Product{code: "A1", price: 10 }).First(&p)

//Map
db.Where(map[string]interface{}{"code":"A1", "price":10}).Find(&p)

//Select * From product where code = "A1". 
//GORM Will only query with non-zero fields, therefore if your field value is 0, '', false or other zero values,it won't be used to build query conditions.
db.Where(&Product{code:"A1", price:0}).Find(&p)
```

Raw SQL 
```go
type Result struct {
    ID int
    Name string
    Age int
}

var result Result
db.Row("SELECT id, name, age FROM users WHERE name =?", 3).Scan(&result)
```

Method Chaining. To view more examples, [click here](https://gorm.io/docs/method_chaining.html)
```go
query := db.Where("code = ?", "A1") 
query.Where("price > ?", 10).First(&p)   // SELECT * from products WHERE code = "A1" AND price > 10
query.Where("price > ?"  15).First(&p2) // SELECT * from products WHERE code = "A1" AND price > 10 AND price > 20

```
### RPC - Protobuf
Google `Protobuf` provides language independence so allow serialization / deserialization that is language independent.
It also provides efficient data compaction. 
A sample `Protobuf` file is provided below with base Data-Types
```protobuf
// Represents the version of Protobuf we ae using
syntax = "proto3";
// Used for conflict resolution if there are multiple members with the same name
package theater;
// Options specific to the generated language. The example below is for generating Java
option java_package = "com.example.theater";

// The theater service definition.
service Theater {
  // ends a rpc method `GetTheater` with `TheaterRequest` and expects `TheaterReply`
  rpc GetTheater (TheaterRequest) returns (TheaterReply) {}
}

// The request message. Base class for the object which would be created
// Attributes of the `TheaterRequest` class with datatype and position of the tag in the schema
// New tags should increment the position integer
message TheaterRequest {
  string name = 1;
  // Numbers
  int32 capacity = 2;
  int64 number = 3;
  float base_price = 4;
  // Boolean
  bool is_available = 5;
  // Enum
  enum PAYMENT_TYPE {
    CASH = 0;
    CREDIT = 1;
    DEBIT = 2;
  }
  PAYMENT_TYPE payment = 6;
  // List
  repeated string snacks = 7;
  // Map
  map<string, int32> ticket_prices = 8;
  // Nested Class
  TheaterOwner owner = 9;
}

message TheaterOwner {
  string name = 1;
  string address = 2;
  string error = 3;
}

// The response message. Base class for the object which would be created
message TheaterReply {
  string message = 1;
}

```
#### RPC Server
```go
type server struct {
    // UnimplementedTheaterServer must be embedded to have forward compatible implementations.
    pb.UnimplementedTheaterServer
}

func (s *server) GetTheater(ctx context.Context, in *pb.TheaterRequest) (*pb.TheaterReply, error) {
    log.Printf("Received: %v", in.GetName())
    return &pb.TheaterReply{Message: "Theater: " + in.GetName()}, nil
}

func main() {
    flag.Parse()
    lis, err := net.Listen("tcp", fmt.Sprintf(":%d", *port))
    if err != nil {...}
    s := grpc.NewServer()
    pb.RegisterTheaterServer(s, &server{})
    log.Printf("server listening at %v", lis.Addr())
    if err := s.Serve(lis); err != nil {
        log.Fatalf("failed to serve: %v", err)
    }
}
```
#### RPC Client
```go
var (
    addr = flag.String("addr", "localhost:50051", "the address to connect to")
    name = flag.String("name", defaultName, "Name of theater")
)

func main() {
	flag.Parse()
	// Set up a connection to the server.
	conn, err := grpc.Dial(*addr, grpc.WithTransportCredentials(insecure.NewCredentials()))
	if err != nil {...}
	defer conn.Close()
	c := pb.NewTheaterClient(conn)

	// Contact the server and print out its response.
	ctx, cancel := context.WithTimeout(context.Background(), time.Second)
	defer cancel()
	r, err := c.getTheater(ctx, &pb.TheaterRequest{
		Name: *name
		...
	})
	if err != nil {...}
	log.Printf("Message: %s", r.GetMessage())
}
```


### Database - MongoDB

Connecting to Mongo and insertion of object sample.
```go
var collection *mongo.Collection

// runs only on init. once
func init() {
	clientOptions := options.Client().ApplyURI(connectionString)
	/*
			Context: Whenever making calls to machines outside your own machine
					 type, deadlines, cancellation signals, other request-scoped-values
					 how long connection, what happens when dies, if active context to work on

			Background: never cancelled, no values, no deadline
			_TODO: Based on the context you are using from
			WithValue: retains copy of parent, only for request-scoped data that transits processes & APIs,
		 			   not for passing optional params to functions
	*/
	client, err := mongo.Connect(context.TODO(), clientOptions)
	helper.CheckNilErr(err)
	fmt.Println("MongoDB connection successful")
	collection = client.Database(dbName).Collection(colName)
	fmt.Println("Collection instance is ready")
}

func insertMovie(movie model.Netflix) primitive.ObjectID {
    result, err := collection.InsertOne(context.Background(), movie)
    helper.CheckNilErr(err)

    return result.InsertedID.(primitive.ObjectID)
}

func InsertMovie(c *gin.Context) {
    var movie = &model.Netflix{}
    err := c.Bind(movie)
    if err != nil {
        c.AbortWithStatus(http.StatusBadRequest)
    return
}

movie.Id = insertMovie(*movie)
c.JSON(http.StatusCreated, movie)

}

```
Simple retrieval sample using `bson.M`.
```go
func getMovie(movieId string) (primitive.M, error) {
	id, _ := primitive.ObjectIDFromHex(movieId)
	filter := bson.M{"_id": id}
	// [Mongo bson]
    // M = shorter & clearer filter declaration, order doesnt matter
    // D = if you have a sort having multiple fields

	result := collection.FindOne(context.Background(), filter)
	var movie primitive.M
	decodeErr := result.Decode(&movie)
	if decodeErr != nil {
		fmt.Println("[Decode_Err]", decodeErr)
		return nil, decodeErr
	}
	return movie, nil
}

func GetMovie(c *gin.Context) {
    // set header
    movie, err := getMovie(c.Params.ByName("id"))
    if len(movie) == 0 && err != nil {
        c.AbortWithError(http.StatusNotFound, err)
        return
    }
    c.JSON(http.StatusOK, movie)
    return
}

---
	
r := gin.Default()

movieGroup := r.Group("/api/movies")
movieGroup.GET("/:id", controller.GetMovie)
log.Fatal(http.ListenAndServe(":8000", r))
```










[//]: # (> [Some-Link-Here]&#40;https://link.me&#41; &nbsp;&middot;&nbsp;)
[//]: # (> [Some-Other-Link]&#40;https://link.me&#41;)