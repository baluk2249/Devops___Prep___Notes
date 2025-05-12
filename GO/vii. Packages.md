
# Go Packages


In Go, a package is a collection of related Go files that are stored in the same directory. The Go standard library is made up of a large set of packages, and creating your own packages allows you to organize and reuse code across multiple Go projects.

Each Go file belongs to a package, and the package name is declared at the top of each file. By convention, the package name usually matches the name of the directory it resides in.

## Structure of a Package

A typical Go package structure looks like this:

```
my_package/
    mypackage.go
    anotherfile.go
    main.go
```

Here:
- `my_package` is the directory that contains Go files.
- `mypackage.go`, `anotherfile.go`, and `main.go` are Go files in the same package.

## Importing Go Packages

In Go, you can import packages into your Go program using the `import` keyword. Importing allows you to access functions, types, and variables from another package.

### Importing a Standard Library Package

You can import a standard Go library package like this:

```go
import "fmt"
```

Example:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go!")
}
```

### Importing a Custom Package

To import a custom package, you provide the path to the package, relative to your GOPATH or module root.

Example (assuming the custom package is in the same directory):

```go
import "./mypackage"
```

Example:

```
my_package/
    main.go
    mypackage/mypackage.go
```

`mypackage.go`:

```go
package mypackage

import "fmt"

func SayHello() {
    fmt.Println("Hello from mypackage!")
}
```

`main.go`:

```go
package main

import "./mypackage"

func main() {
    mypackage.SayHello()
}
```

### Importing Multiple Packages

Go supports importing multiple packages in a single import block:

```go
import (
    "fmt"
    "math"
)
```

## Creating a Package

To create your own package in Go, follow these steps:

1. Create a directory for your package.
2. Inside the directory, create a `.go` file.
3. Define the package at the top of the file (e.g., `package mypackage`).
4. Add functions or types you want to export (make them start with an uppercase letter).

Example:

Directory structure:

```
my_package/
    main.go
    mypackage/
        mypackage.go
```

`mypackage.go`:

```go
package mypackage

import "fmt"

// Exported function (starts with uppercase letter)
func SayHello() {
    fmt.Println("Hello from mypackage!")
}

// Unexported function (starts with lowercase letter)
func sayGoodbye() {
    fmt.Println("Goodbye!")
}
```

`main.go`:

```go
package main

import "my_package/mypackage"

func main() {
    mypackage.SayHello() // Accessible because it is exported
    // mypackage.sayGoodbye() // Error: cannot access unexported function
}
```

## Built-in Go Packages

Go comes with many built-in packages for common tasks, such as:

- `fmt` for formatted I/O operations.
- `os` for interacting with the operating system.
- `strings` for string manipulation.
- `math` for mathematical functions.
- `net/http` for HTTP client and server.

Example using the `strings` package:

```go
package main

import (
    "fmt"
    "strings"
)

func main() {
    str := "hello, world"
    fmt.Println(strings.ToUpper(str)) // Outputs: HELLO, WORLD
}
```

## Exporting and Importing

In Go, only functions, variables, and types that start with an uppercase letter are exported, meaning they can be accessed from other packages.

Example:

```go
package mypackage

// Exported function (accessible from other packages)
func Greet(name string) string {
    return "Hello, " + name
}

// Unexported function (cannot be accessed from other packages)
func secret() string {
    return "This is a secret!"
}
```

## Conclusion

Go packages are an essential part of organizing and reusing code. They allow for clean, modular code by grouping related functions and types into manageable units. By understanding the structure and import mechanisms, you can write well-organized and maintainable Go code.