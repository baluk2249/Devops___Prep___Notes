# Loops 

Go provides a simple yet powerful looping mechanism using the `for` keyword. It is the only looping construct in Go, but it can be used in different ways to achieve all common looping needs.

---

## ✅ Basic `for` Loop

### Syntax:

```go
for initialization; condition; post {
    // code block
}
```

### Example:

```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```

---

## 🔁 While-style Loop

When you skip the initialization and post statements, the `for` loop works like a `while` loop.

### Example:

```go
i := 0
for i < 5 {
    fmt.Println(i)
    i++
}
```

---

## 🔁 Infinite Loop

To create an infinite loop, just use `for` without any condition:

### Example:

```go
for {
    fmt.Println("Running forever")
    // Add a break condition inside if needed
    break
}
```

---

## 🔁 Looping Over Collections

### 🔹 Looping over Arrays or Slices

```go
nums := []int{1, 2, 3, 4}
for index, value := range nums {
    fmt.Printf("Index: %d, Value: %d\n", index, value)
}
```

### 🔹 Looping over Maps

```go
person := map[string]string{
    "name": "Alice",
    "city": "Wonderland",
}
for key, value := range person {
    fmt.Printf("%s: %s\n", key, value)
}
```

### 🔹 Looping over Strings (runes)

```go
str := "hello"
for i, char := range str {
    fmt.Printf("Index: %d, Char: %c\n", i, char)
}
```

---

## ⏹ Using `break` and `continue`

### 🔹 `break`

Used to exit the loop prematurely.

```go
for i := 0; i < 10; i++ {
    if i == 5 {
        break
    }
    fmt.Println(i)
}
```

### 🔹 `continue`

Skips the current iteration and continues with the next.

```go
for i := 0; i < 5; i++ {
    if i%2 == 0 {
        continue
    }
    fmt.Println(i)
}
```

---

## 🔄 Nested Loops

You can nest loops inside other loops:

```go
for i := 1; i <= 3; i++ {
    for j := 1; j <= 2; j++ {
        fmt.Printf("i: %d, j: %d\n", i, j)
    }
}
```

---

## 📌 Summary Table

| Loop Type        | Example Code Snippet         |
| ---------------- | ---------------------------- |
| Classic for      | `for i := 0; i < n; i++ {}`  |
| While-style      | `for condition {}`           |
| Infinite         | `for {}`                     |
| Range over slice | `for i, v := range slice {}` |
| Range over map   | `for k, v := range map {}`   |
| Break            | `if condition { break }`     |
| Continue         | `if condition { continue }`  |

---
