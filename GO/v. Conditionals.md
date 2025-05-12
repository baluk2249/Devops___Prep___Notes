# Conditionals 

Go supports standard conditional statements like `if`, `else if`, and `else` to control the flow of a program. It also supports `switch` statements for more complex branching.

---

## ✅ `if` Statement

### Syntax:

```go
if condition {
    // code block
}
```

### Example:

```go
x := 10
if x > 5 {
    fmt.Println("x is greater than 5")
}
```

---

## 🔁 `if-else` Statement

### Example:

```go
x := 3
if x%2 == 0 {
    fmt.Println("Even number")
} else {
    fmt.Println("Odd number")
}
```

---

## 🔄 `if-else if-else` Ladder

### Example:

```go
score := 85
if score >= 90 {
    fmt.Println("Grade: A")
} else if score >= 75 {
    fmt.Println("Grade: B")
} else if score >= 60 {
    fmt.Println("Grade: C")
} else {
    fmt.Println("Grade: F")
}
```

---

## 📦 Short Statement with `if`

Go allows you to declare and initialize variables within the `if` condition.

### Example:

```go
if age := 18; age >= 18 {
    fmt.Println("Adult")
}
```

---

## 🔀 `switch` Statement

The `switch` statement is a cleaner alternative to many `if-else-if` statements.

### Syntax:

```go
switch expression {
case value1:
    // code
case value2:
    // code
default:
    // default code
}
```

### Example:

```go
day := "Tuesday"
switch day {
case "Monday":
    fmt.Println("Start of the week")
case "Friday":
    fmt.Println("End of the week")
default:
    fmt.Println("Midweek day")
}
```

---

## 🔁 Switch with Multiple Cases

### Example:

```go
ch := 'a'
switch ch {
case 'a', 'e', 'i', 'o', 'u':
    fmt.Println("Vowel")
default:
    fmt.Println("Consonant")
}
```

---

## 🌀 Switch Without Expression

You can omit the switch expression to write clean branching logic.

### Example:

```go
num := 7
switch {
case num < 0:
    fmt.Println("Negative")
case num == 0:
    fmt.Println("Zero")
default:
    fmt.Println("Positive")
}
```

---

## 🔁 `fallthrough` Keyword

Allows execution to fall through to the next case.

### Example:

```go
num := 1
switch num {
case 1:
    fmt.Println("One")
    fallthrough
case 2:
    fmt.Println("Two")
}
```

---

