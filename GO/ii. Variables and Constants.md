# Go Variables and Constants


---

## 🔸 Variables in Go

Variables in Go are used to store values of different types. They are **statically typed**, meaning their type is determined at compile time.

### ✅ Declaring Variables

#### 1. Using `var` keyword

```go
var age int = 25
var name string = "Alice"
```

#### 2. Type inference (without specifying the type)

```go
var city = "New York"  // Go infers it as string
```

#### 3. Short variable declaration (inside functions only)

```go
count := 10
isActive := true
```

### 📌 Multiple Variable Declaration

```go
var a, b, c int = 1, 2, 3
name, age := "Bob", 30
```

### 📌 Default Zero Values

If variables are declared without initialization, they are assigned **zero values**:

* `0` for numeric types
* `false` for booleans
* `""` (empty string) for strings
* `nil` for pointers, interfaces, slices, etc.

```go
var x int        // x = 0
var y string     // y = ""
var z bool       // z = false
```

### 📌 Scope of Variables

* **Local**: declared inside a function
* **Package-level**: declared outside any function

```go
var globalVar = "Visible in the whole package"

func main() {
    var localVar = "Visible only in main"
    fmt.Println(globalVar, localVar)
}
```

---

## 🔸 Constants in Go

Constants are used for values that **do not change** during program execution. They are declared using the `const` keyword.

### ✅ Declaring Constants

```go
const Pi = 3.14
const Greeting = "Hello, Go!"
```

### 🔸 Typed and Untyped Constants

#### Typed:

```go
const a int = 10
```

#### Untyped:

```go
const b = 10   // Can be used flexibly across types
```

### 📌 Arithmetic with Constants

```go
const x = 5
const y = x * 2  // Valid
```

### 📌 Grouped Constants

```go
const (
    North = 0
    East  = 1
    South = 2
    West  = 3
)
```

### 📌 `iota` in Constants

`iota` is a special identifier used in const declarations to simplify definitions:

```go
const (
    A = iota  // 0
    B         // 1
    C         // 2
)
```

You can use it for enums and bitmasks:

```go
const (
    Read = 1 << iota  // 1
    Write             // 2
    Execute           // 4
)
```

---

## 🧪 Code Examples

### Example 1: Variables

```go
package main

import "fmt"

func main() {
    var name = "John"
    age := 30
    fmt.Println("Name:", name, "Age:", age)
}
```

### Example 2: Constants

```go
package main

import "fmt"

const Pi = 3.1415
const Greeting = "Hello"

func main() {
    fmt.Println(Greeting, "Pi is", Pi)
}
```

---

## 📌 Summary

| Concept   | Description                            | Example            |
| --------- | -------------------------------------- | ------------------ |
| Variable  | Mutable named storage                  | `var x int = 5`    |
| Constant  | Immutable value                        | `const Pi = 3.14`  |
| iota      | Auto-incrementing constant generator   | `const (A = iota)` |
| Short Var | Concise syntax for function scope vars | `name := "Go"`     |

---
