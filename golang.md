GOLANG
:go:golang:

# TOC
- [TOC](#toc)
- [Other CheatSheets](#other-cheatsheets)
- [Intro](#intro)
- [Packages - Imports - Comments](#packages---imports---comments)
- [Vars - Data Types - Constants](#vars---data-types---constants)
- [Arithmetic Operations](#arithmetic-operations)
- [Taking Input](#taking-input)
- [If - Else - Switch](#if---else---switch)
- [Loops](#loops)
- [Functions - Deferring - Scope](#functions---deferring---scope)
- [Methods](#methods)
- [Pointers](#pointers)
- [Structs](#structs)
- [Arrays - Ranges - Maps](#arrays---ranges---maps)
- [Variadic Functions](#variadic-functions)
- [Make](#make)
- [Goroutines and Channels](#goroutines-and-channels)
- [Select](#select)
- [API Calls](#api-calls)
  - [GET request](#get-request)
  - [POST request](#post-request)
  - [Setting Headers:](#setting-headers)
  - [Handling Redirects](#handling-redirects)
  - [Customizing the Request](#customizing-the-request)
  - [Authentication](#authentication)
    - [API Key](#api-key)
    - [Basic Authentication](#basic-authentication)
    - [OAuth 2.0](#oauth-20)
- [Compiling](#compiling)
- [Best Practices](#best-practices)
  - [Packages](#packages)
  - [Interfaces](#interfaces)
  - [Error Handling](#error-handling)
  - [TDD - Test Drive Development](#tdd---test-drive-development)
    - [TDD in Go](#tdd-in-go)
    - [Running Tests in Go](#running-tests-in-go)


# Other CheatSheets

There are many Go cheatsheets available online, some of the popular ones are:

    [Go by Example](https://gobyexample.com)
    [A Tour of Go](https://tour.golang.org/welcome/1)
    [Go Bootcamp](https://gobootcamp.com/book/exercises)
    [Go Lang Cheatsheet](https://devhints.io/go)
    [Go Cheatsheet](https://github.com/a8m/go-lang-cheat-sheet)
    [Go Lang Ref Card](https://go-lang-cheat-sheet.readthedocs.io/en/latest/)
    [Go Lang Quick Guide](https://www.tutorialspoint.com/go/go_quick_guide.htm)


These resources provide concise and comprehensive information on Go language syntax, data structures, and standard library functions.

# Intro

Go cheat sheet which will include syntax for:

* Packages, import, comments
* Vars, data types, constants, arythmetic operations, relational and logical operations
* Taking input, if / else, switch, loops
* Functions, deferring, scope, methods
* Pointers, structs, 
* Arrays, ranges, maps, variadic functions,
* Goroutines, channels, select



Besides the syntax, you need to be familiar with Go's standard library, testing, error handling, and concurrent programming.

    * Go Standard Library: It provides a wide range of functionality including string manipulation, I/O operations, networking, cryptography, and more. Familiarize yourself with the most commonly used packages.
    * Testing: Go has built-in support for testing and provides the testing package for writing and executing tests. It's important to write tests for your code to ensure it's working as expected.
    * Error handling: Go uses errors as first-class values and encourages returning errors from functions to handle them. It's essential to be familiar with Go's error handling approach to write robust and reliable code.
    * Concurrent programming: Go's concurrency primitives (goroutines and channels) make it easy to write concurrent code that can handle multiple tasks in parallel.

Additionally, understanding the Go programming paradigms and idioms, such as Go's strict typing, garbage collection, and the concept of passing values by value rather than reference, is important in writing production-ready Go code.

# Packages - Imports - Comments

    Packages, import, comments: Go code is organized in packages. The main function has to be in the main package. Import allows to use code from other packages, and comments are added to explain the code.
    
    Package declaration starts at the first line of the code, it specifies the name of the package.
    A package is a collection of Go source files in the same directory that are built together.

```go
package main
```

Import:

    Import statement is used to import external packages in the code.

```go
import "fmt"
```

Comments:

    Single line comments start with //.
    Multi-line comments start with /* and end with */.

```go
// single line comment

/* 
  multi-line
  comment 
*/
```

# Vars - Data Types - Constants

    Vars, data types, constants, arithmetic operations, relational and logical operations: Variables in Go have a type and can be declared with the var keyword. Data types include int, float, string, etc. Constants are defined using the const keyword and arithmetic and relational operations can be performed on variables.
    
    In Go, in addition to the basic types (bool, string, int, float64, etc.), there are also composite types such as arrays, slices, maps, structs, and pointers. There are also more advanced types such as interfaces, channels, and functions, which are used for more specialized use cases.
    
    Variables can be declared using var keyword.
    Data types include int, float, string, bool, etc.
    Constants are declared using the const keyword.

```go
var x int = 10
const y = 20
```

# Arithmetic Operations

    Go supports the standard arithmetic operations: +, -, *, /, %.

Relational and Logical Operations:

    Go supports the standard relational operations: ==, !=, <, >, <=, >=.
    Go supports the standard logical operations: &&, ||, !.

# Taking Input

    Taking input, if/else, switch, loops: Go has a standard library for reading input from the user. 
    
    Input can be taken using fmt.Scanln or fmt.Scanf.

```go
var n int
fmt.Scanln(&n)
```

# If - Else - Switch

If/else and switch statements control the flow of the program.

    If/Else statements are used to execute different code blocks based on the conditions.

```go
if x > 10 {
  fmt.Println("x is greater than 10")
} else {
  fmt.Println("x is less than or equal to 10")
}
```

Switch:

    Switch statements are used to execute different code blocks based on multiple conditions.

```go
switch n {
case 1:
  fmt.Println("One")
case 2:
  fmt.Println("Two")
default:
  fmt.Println("Unknown")
}
```

# Loops
 
 Loops allow to repeat code blocks.
 
    Go supports for and while loops.

```go
for i := 0; i < 10; i++ {
  fmt.Println(i)
}

for {
  // infinite loop
}

x := 0
for x < 10 {
  fmt.Println(x)
  x++
}
```

# Functions - Deferring - Scope

    Functions, deferring, scope: Functions are blocks of code that can be executed from other parts of the program. Deferring delays the execution of a function until the surrounding function returns.
    
    Functions are declared using the func keyword.

```go
func add(a int, b int) int {
  return a + b
}
```

Deferring:

    defer keyword is used to execute a function after the surrounding function returns.

```go
func main() {
  defer fmt.Println("World")
  fmt.Println("Hello")
}
```

Scope:

    Variables declared inside a function are not accessible outside the function.

# Methods

 Methods are functions attached to a specific type, they can access and modify the fields of the type they belong to.
 
    Methods are functions attached to a specific type.
    

```go
type Circle struct {
  radius float64
}

func (c Circle) Area() float64 {
  return math.Pi * c.radius * c.radius
}

func main() {
  c := Circle{radius: 5}
  fmt.Println("Area of Circle:", c.Area())
}
```

# Pointers

    Pointers: Pointers are variables that store the memory address of another value.
    
```go
func zero(x *int) {
  *x = 0
}

func main() {
  x := 5
  zero(&x)
  fmt.Println(x) // Output: 0
}
```
# Structs

Structs are user-defined types that group together values with different types.

```go
type Person struct {
  Name string
  Age  int
}

func main() {
  p := Person{Name: "John", Age: 25}
  fmt.Println(p)
}
```

See Methods below.

# Arrays - Ranges - Maps

    Arrays, ranges, maps, variadic functions: Arrays are fixed-length sequences of values of the same type. Ranges allow to iterate over the elements of arrays, maps and slices. Maps store key-value pairs and can be used as dictionaries. Variadic functions can take a variable number of arguments.
    
```go
func main() {
  // Arrays
  a := [3]int{1, 2, 3}
  fmt.Println(a)

  // Ranges
  for i, v := range a {
    fmt.Println(i, v)
  }

  // Maps
  m := map[string]int{"one": 1, "two": 2}
  fmt.Println(m)
}
```

# Variadic Functions

A variadic function is a function that can accept a variable number of arguments. In Go, this is indicated by an ellipsis (...) in the function definition before the type of the variadic parameter. The arguments passed to the function can be accessed within the function as a slice. Variadic functions are often used to handle a variable number of inputs of the same type.

```go
func sum(nums ...int) {
  total := 0
  for _, v := range nums {
    total += v
  }
  fmt.Println(total)
}

func main() {
  sum(1, 2, 3)
}
```
# Make

`make` can be used for creating slices, maps, and channels.

For example, to create a slice:

```go
s := make([]int, 0, 5)
```

To create a map:

```go
m := make(map[string]int)
```

And to create a channel:

```go
c := make(chan int)
```

It's important to note that make only initializes the specified data structure and doesn't make any other changes to it. It's commonly used to allocate a zeroed data structure with a specified length, capacity, or both.

# Goroutines and Channels

    Goroutines, channels: Goroutines are light-weight threads. Channels allow communication between goroutines and can be used to synchronize their execution. 
    
```go
func sum(a, b int, c chan int) {
  c <- a + b
}

func main() {
  c := make(chan int)
  go sum(1, 2, c)
  fmt.Println(<-c)
}
```

# Select

Select statement allows to wait on multiple channels.

```go
func main() {
  c1 := make(chan string)
  c2 := make(chan string)

  go func() {
    time.Sleep(time.Second * 1)
    c1 <- "one"
  }()

  go func() {
    time.Sleep(time.Second * 2)
    c2 <- "two"
  }()

  for i := 0; i < 2; i++ {
    select {
    case msg1 := <-c1:
      fmt.Println("received", msg1)
    case msg2 := <-c2:
      fmt.Println("received", msg2)
    default:
      fmt.Println("No value received from channel")
    }
  }
}
```
# API Calls

To make an API call in Golang, you can use the built-in "net/http" package.

## GET request

```go
package main

import (
    "fmt"
    "io/ioutil"
    "net/http"
)

func main() {
    resp, err := http.Get("https://api.example.com/endpoint")
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()

    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        panic(err)
    }

    fmt.Println(string(body))
}
```

## POST request

```go
package main

import (
    "bytes"
    "fmt"
    "io/ioutil"
    "net/http"
)

func main() {
    data := []byte("request body data")

    resp, err := http.Post("https://api.example.com/endpoint", "application/json", bytes.NewBuffer(data))
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()

    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        panic(err)
    }

    fmt.Println(string(body))
}
```

## Setting Headers:

```go
package main

import (
    "fmt"
    "io/ioutil"
    "net/http"
)

func main() {
    req, err := http.NewRequest("GET", "https://api.example.com/endpoint", nil)
    if err != nil {
        panic(err)
    }
    req.Header.Set("User-Agent", "my-app")
    req.Header.Set("Authorization", "Bearer my-token")

    client := &http.Client{}
    resp, err := client.Do(req)
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()

    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        panic(err)
    }

    fmt.Println(string(body))
}
```

## Handling Redirects

```go
package main

import (
    "fmt"
    "io/ioutil"
    "net/http"
)

func main() {
    client := &http.Client{
        CheckRedirect: func(req *http.Request, via []*http.Request) error {
            // handle redirects here, e.g. limit the number of redirects
            return nil
        },
    }

    resp, err := client.Get("https://api.example.com/endpoint")
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()

    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        panic(err)
    }

    fmt.Println(string(body))
}
```

## Customizing the Request

```go
package main

import (
    "fmt"
    "io/ioutil"
    "net/http"
    "net/url"
    "time"
)

func main() {
    client := &http.Client{
        Timeout: time.Second * 10,
    }

    values := url.Values{
        "param1": {"value1"},
        "param2": {"value2"},
    }

    req, err := http.NewRequest("GET", "https://api.example.com/endpoint", nil)
    if err != nil {
        panic(err)
    }

    // Customize the request headers
    req.Header.Set("User-Agent", "my-app")
    req.Header.Set("Authorization", "Bearer my-token")

    // Add query parameters to the URL
    req.URL.RawQuery = values.Encode()

    // Make the request
    resp, err := client.Do(req)
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()

    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        panic(err)
    }

    fmt.Println(string(body))
}
```

## Authentication

There are several ways to authenticate to an API in Go, depending on the API and the authentication method it supports.

Some common authentication methods include:

### API Key

This method involves passing an API key as a request header or query parameter. The server then verifies the key and grants access if it is valid.

```go
req, err := http.NewRequest("GET", "https://api.example.com/endpoint", nil)
if err != nil {
    panic(err)
}

req.Header.Set("Authorization", "Bearer my-api-key")

resp, err := http.DefaultClient.Do(req)
if err != nil {
    panic(err)
}
```

### Basic Authentication

This method involves passing a username and password encoded in Base64 as a request header.

```go
req, err := http.NewRequest("GET", "https://api.example.com/endpoint", nil)
if err != nil {
    panic(err)
}

req.SetBasicAuth("username", "password")

resp, err := http.DefaultClient.Do(req)
if err != nil {
    panic(err)
}
```

### OAuth 2.0

This method is a widely used authentication and authorization framework that allows applications to obtain access to a user's resources without having to store their passwords.

```go
func getToken() (string, error) {
    // obtain the OAuth2 token
}

func makeAPIRequest() error {
    token, err := getToken()
    if err != nil {
        return err
    }

    req, err := http.NewRequest("GET", "https://api.example.com/endpoint", nil)
    if err != nil {
        return err
    }

    req.Header.Set("Authorization", "Bearer "+token)

    resp, err := http.DefaultClient.Do(req)
    if err != nil {
        return err
    }

    return nil
}
```

# Compiling


Simple compiling command will match the binary to the architecture and the os you are running it on:

```go
go build main.go
```

Go provides a solution for cross-compilation feature. You can use the GOOS and GOARCH environment variables to specify the target operating system and architecture, respectively.

For example, to compile a binary for Linux on a Windows machine, you can run:

```go
GOOS=linux GOARCH=amd64 go build main.go
```

Most common OS types and architectures (the full list is available in the docs):

```diff
GOOS    GOARCH
----    ------
darwin  amd64
linux   amd64
windows amd64

GOOS    GOARCH
----    ------
android arm
linux   arm

GOOS    GOARCH
----    ------
windows 386
```


# Best Practices

Go is designed to encourage good software design practices, so there are several best practices that can help you write clear, maintainable, and efficient code. Here are some of the most important ones:

* Keep it simple: Go is designed to be simple, so aim for simplicity in your code. Write straightforward code that is easy to understand, and avoid complicated abstractions or design patterns unless they're absolutely necessary.
* Modularity: Divide your program into smaller, well-defined pieces, and make use of Go's packages to organize your code. This makes it easier to maintain and test your code.
* Consistent naming: Use descriptive, meaningful, and consistent names for your functions, variables, and types. This makes your code easier to read and understand.
Interfaces: Make use of Go's interfaces to write code that is decoupled from its implementation. This makes it easier to test your code and swap out implementations as needed.
* Error handling: Go has a strong emphasis on error handling, and it's important to handle errors properly in your code. Return errors as early as possible and make use of Go's built-in error types to write clear and meaningful error messages.
* Test-driven development: Write tests for your code, and aim for high test coverage. This helps you catch bugs early and ensures that your code is reliable and robust.
* Documentation: Write clear and concise documentation for your code, and make use of Go's built-in documentation tools. This makes it easier for others to understand and use your code.

By following these best practices, you can write high-quality Go code that is maintainable, testable, and scalable.

## Packages

Go uses packages to organize code and provide modularity. A package is a collection of related Go source files that define functions, types, and variables.

To define a new package, you can simply add a package declaration at the top of each source file in the package. For example:

```go
package mypackage

func MyFunction() {
    // function implementation
}
```

Go has a number of built-in packages, and you can also import third-party packages or create your own. To import a package, you can use the import statement. For example:

```go
import (
    "fmt"
    "mypackage"
)

func main() {
    fmt.Println("Hello, world!")
    mypackage.MyFunction()
}
```

By organizing your code into packages, you can make your code easier to understand, maintain, and reuse. Packages also allow you to define and use abstractions, which can help you write code that is more flexible and adaptable to change.

In Go, the location of a package file depends on the GOPATH environment variable. GOPATH is an environment variable that specifies the location of your Go workspace, which contains your Go source code, packages, and compiled binaries.

By default, GOPATH is set to a directory named go in your home directory. The Go tools expect your package files to be located within the src subdirectory of the GOPATH directory.

For example, if your GOPATH is set to /home/user/go, and you have a package named mypackage in a directory /home/user/go/src/github.com/myuser/mypackage, then you can import that package in your Go program using the following import statement:

```go
import "github.com/myuser/mypackage"
```

In this example, the package is located in the github.com/myuser/mypackage directory, which is relative to the src directory in the GOPATH.

When you run the go install command, the Go tools will compile the package and store the compiled binary in the bin directory under the GOPATH. The compiled binary can then be imported and used by other Go programs.

## Interfaces

In Go, an interface defines a set of methods that a type must implement to be considered "compatible" with the interface. Interfaces allow you to write code that is decoupled from the implementation of the type.

Here's an example of how you might define an interface in Go:

```go
type Shape interface {
    Area() float64
    Perimeter() float64
}
```

In this example, the Shape interface defines two methods, Area and Perimeter, that must be implemented by any type that wants to be considered a Shape.

To implement an interface in Go, a type must provide a concrete implementation of all the methods defined by the interface. For example, here's how you might implement the Shape interface for a rectangle:

```go
type Rectangle struct {
    width  float64
    height float64
}

func (r Rectangle) Area() float64 {
    return r.width * r.height
}

func (r Rectangle) Perimeter() float64 {
    return 2 * (r.width + r.height)
}
```

In this example, the Rectangle type implements the Shape interface by providing implementations of the Area and Perimeter methods.

Interfaces are a powerful mechanism in Go that can help you write flexible, modular, and testable code. By defining interfaces and using them to decouple your code from the implementation of the types, you can write code that is more flexible and adaptable to change.

## Error Handling

In Go, errors are represented as values of the built-in error type, which is a simple interface that defines a single method, Error() string. To indicate that a function has failed, you can return an error value from the function.

Here's an example of how you might handle an error in Go:

```go
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }
    return a / b, nil
}

func main() {
    result, err := divide(10, 2)
    if err != nil {
        fmt.Println("error:", err)
        return
    }
    fmt.Println("result:", result)
}
```

In this example, the divide function returns an error if the denominator b is zero. The error is returned as a value of type error and can be checked by the calling code. If the error is not nil, then the error message can be printed.

The fmt.Errorf function is used to create a new error value with a formatted error message. There are many other functions in Go's standard library that return error values, such as os.Open, json.Unmarshal, and so on.

In Go, it's common to return an error as the last return value of a function, and to check the error value immediately after calling the function. This pattern is so common in Go that it's often referred to as the "error-checking idiom".

## TDD - Test Drive Development

Test-Driven Development (TDD) is a software development process that emphasizes writing tests before writing production code. The basic idea is to write a test for a small piece of functionality, then write the minimum amount of code necessary to make the test pass. This process is then repeated until all of the desired functionality has been implemented and tested.

Here's an overview of the TDD process:

* Write a test: Start by writing a test for a small piece of functionality that you want to implement. The test should fail initially, since the implementation hasn't been written yet.
* Write the minimum amount of code necessary to make the test pass: Write the minimum amount of code necessary to make the test pass. The code should only implement the functionality that's required to pass the test.
* Refactor: Once the test is passing, you can refactor the code if necessary to make it cleaner and more maintainable.
* Repeat: Repeat the process of writing tests and implementing the minimum amount of code necessary to make the tests pass, until all of the desired functionality has been implemented and tested.

By following the TDD process, you can ensure that your code is well tested and that you are only implementing the functionality that you actually need. TDD also helps to ensure that your code is maintainable and easy to understand, since you are writing small, focused tests and writing the minimum amount of code necessary to make the tests pass.

It's important to note that TDD is not just about writing tests. It's about using tests to drive the design and development of your code. By writing tests first, you are forced to think about the interface and behavior of your code before you start writing the implementation. This can lead to a better design and a more maintainable codebase.

### TDD in Go

In Go, you can do Test-Driven Development (TDD) by writing tests for your code using the built-in testing package. The testing package provides a simple and flexible way to write and run tests for your Go code.

Here's an example of how you might do TDD in Go:

* Write a test: Start by writing a test for a small piece of functionality that you want to implement. In Go, tests are functions with names starting with Test that are defined in a separate file with a _test.go suffix. For example:

```go
func TestDivide(t *testing.T) {
    result, err := Divide(10, 2)
    if err != nil {
        t.Errorf("Unexpected error: %v", err)
    }
    if result != 5 {
        t.Errorf("Expected result to be 5, but got %v", result)
    }
}
```

* Write the minimum amount of code necessary to make the test pass: Write the minimum amount of code necessary to make the test pass. For example:

```go
func Divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }
    return a / b, nil
}
```

* Run the test: Run the test using the go test command to see if it passes or fails.
* Refactor: Once the test is passing, you can refactor the code if necessary to make it cleaner and more maintainable.

* Repeat: Repeat the process of writing tests and implementing the minimum amount of code necessary to make the tests pass, until all of the desired functionality has been implemented and tested.

By following this process, you can ensure that your code is well tested and that you are only implementing the functionality that you actually need. The testing package provides a number of useful functions and techniques for writing tests, such as the ability to test multiple scenarios in a single test function, and the ability to test private functions by using a separate file with a _test.go suffix.

### Running Tests in Go

In Go, test files are typically located in the same package as the code they are testing and have a _test.go suffix. For example, if you have a package example that contains your code, you would create a file example_test.go to hold your tests.

The Go tooling is designed to automatically discover and run tests located in files with a _test.go suffix within the same package as the code being tested. You can run the tests for a package using the go test command, and it will automatically discover and run all of the tests in the package.

For example, if you have a file example.go with the following code:

```go
package example

func Add(a, b int) int {
    return a + b
}
```

You would create a file example_test.go with the following code:

```go
package example

import "testing"

func TestAdd(t *testing.T) {
    result := Add(1, 2)
    if result != 3 {
        t.Errorf("Expected result to be 3, but got %v", result)
    }
}
```

And then you could run the tests with the go test command, and it would automatically discover and run the TestAdd function defined in the example_test.go file.


```go

```

```go

```


```go

```