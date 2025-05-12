# Go Data Types 


---

## ✅ Basic Data Types

### 🔹 Numeric Types

#### Integers

* Signed: `int`, `int8`, `int16`, `int32`, `int64`
* Unsigned: `uint`, `uint8`, `uint16`, `uint32`, `uint64`
* Alias: `byte` (alias for `uint8`), `rune` (alias for `int32`)

```go
var a int = 10
var b uint8 = 255
var c byte = 'A'
var d rune = '😊'
```

#### Floating-Point

* `float32`, `float64`

```go
var f1 float32 = 3.14
var f2 float64 = 2.718281828
```

#### Complex Numbers

* `complex64` (contains two float32)
* `complex128` (contains two float64)

```go
var c1 complex64 = 1 + 2i
var c2 = complex(3.5, 4.5)
```

### 🔹 Boolean Type

```go
var isActive bool = true
```

### 🔹 String Type

Strings are immutable sequences of bytes.

```go
var name string = "Golang"
fmt.Println(name[0])        // Output: 71 (ASCII of 'G')
fmt.Println(string(name[0])) // Output: G
```

---

## ✅ Composite Data Types

### 🔸 Array

Fixed-size collection of elements of the same type.

```go
var arr [3]int = [3]int{1, 2, 3}
fmt.Println(arr[0])
```

### 🔸 Slice

Dynamic-size, more common than arrays.

```go
nums := []int{10, 20, 30}
nums = append(nums, 40)
```

### 🔸 Map

Key-value pairs.

```go
person := map[string]string{
    "name": "Alice",
    "city": "Wonderland",
}
fmt.Println(person["city"])
```

### 🔸 Struct

Used to group related fields.

```go
type Person struct {
    Name string
    Age  int
}

p := Person{Name: "John", Age: 30}
fmt.Println(p.Name)
```

---

## ✅ Special Data Types

### 🔸 Pointer

Stores memory address of a variable.

```go
var x = 42
var p *int = &x
fmt.Println(*p) // Dereferencing pointer
```

### 🔸 Interface

Used to define behavior with method signatures.

```go
type Animal interface {
    Speak() string
}
```

### 🔸 Function Type

```go
func greet(name string) string {
    return "Hello, " + name
}

var f func(string) string = greet
fmt.Println(f("Bob"))
```

---

## 📌 Type Conversion

Go doesn’t support implicit type conversion. Use explicit conversion:

```go
var a int = 10
var b float64 = float64(a)
```

---

## 📌 Summary Table

| Category   | Types & Examples                   |
| ---------- | ---------------------------------- |
| Numeric    | `int`, `float64`, `complex128`     |
| Boolean    | `bool`, e.g., `true`, `false`      |
| String     | `string`, e.g., `"Go"`             |
| Composite  | `array`, `slice`, `map`, `struct`  |
| Special    | `pointer`, `interface`, `function` |
| Conversion | `float64(x)`, `int(y)`             |

---
