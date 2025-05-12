# Functions in Go (Golang)

Functions in Go are **first-class citizens**, meaning they can be assigned to variables, passed as arguments, and returned from other functions. Functions are used to organize and reuse code.

---

## ✅ Defining a Function

### Syntax:

```go
func functionName(parameterList) returnType {
    // function body
}
```

### Example:

```go
func greet(name string) string {
    return "Hello, " + name
}

func main() {
    message := greet("Alice")
    fmt.Println(message)
}
```

---

## 🔢 Multiple Parameters

```go
func add(a int, b int) int {
    return a + b
}
```

If multiple parameters have the same type, you can shorten the declaration:

```go
func add(a, b int) int {
    return a + b
}
```

---

## 🔁 Multiple Return Values

Go functions can return more than one value.

### Example:

```go
func divide(a, b int) (int, int) {
    return a / b, a % b
}

func main() {
    q, r := divide(10, 3)
    fmt.Println("Quotient:", q)
    fmt.Println("Remainder:", r)
}
```

---

## 📦 Named Return Values

You can name the return variables and use a `return` statement without arguments.

### Example:

```go
func fullName() (first string, last string) {
    first = "John"
    last = "Doe"
    return
}
```

---

## 🔃 Variadic Functions

Functions that accept a variable number of arguments.

### Example:

```go
func sum(numbers ...int) int {
    total := 0
    for _, n := range numbers {
        total += n
    }
    return total
}

func main() {
    fmt.Println(sum(1, 2, 3, 4))
}
```

---

## 🧠 Anonymous Functions

Functions without a name, often used as literals.

### Example:

```go
func main() {
    add := func(a, b int) int {
        return a + b
    }
    fmt.Println(add(5, 3))
}
```

---

## 🔄 Passing Functions as Arguments

```go
func apply(op func(int, int) int, a, b int) int {
    return op(a, b)
}

func main() {
    result := apply(func(x, y int) int { return x + y }, 3, 4)
    fmt.Println(result)
}
```

---

## 🔁 Recursive Functions

Functions that call themselves.

### Example:

```go
func factorial(n int) int {
    if n == 0 {
        return 1
    }
    return n * factorial(n-1)
}

func main() {
    fmt.Println(factorial(5)) // Output: 120
}
```

---

