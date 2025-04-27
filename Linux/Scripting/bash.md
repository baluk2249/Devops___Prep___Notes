# 📜 Bash Scripting

## 1. What is Bash?
- **Bash** = Bourne Again Shell.
- It's a **command-line interpreter** and **scripting language** for Linux/Unix systems.
- Executes commands from a terminal or from a file (script).

---

## 2. Basics of Bash Scripts
- A script is a text file containing Bash commands.
- **Start every script with a shebang**:  
  ```bash
  #!/bin/bash
  ```
- **Make it executable**:
  ```bash
  chmod +x script.sh
  ./script.sh
  ```

---

## 3. Variables
- Declare and assign:
  ```bash
  name="Alice"
  age=25
  ```
- No spaces around `=`.
- Use `$` to access:
  ```bash
  echo "My name is $name"
  ```
- **Best practice**: use `{}` around variables:
  ```bash
  echo "Hello, ${name}!"
  ```

---

## 4. User Input
- Read user input:
  ```bash
  read -p "Enter your name: " username
  echo "Hello, $username"
  ```

---

## 5. Conditionals (`if` statements)
- Basic `if`:
  ```bash
  if [ condition ]; then
    # commands
  fi
  ```
- Example:
  ```bash
  if [ "$age" -ge 18 ]; then
    echo "Adult"
  else
    echo "Minor"
  fi
  ```

### Operators

| Type | Operator |
|:---|:---|
| Numeric | -eq, -ne, -lt, -le, -gt, -ge |
| String | =, !=, -z (empty), -n (not empty) |
| File | -e (exists), -d (directory), -f (file), -r (readable), -w (writable), -x (executable) |

---

## 6. Loops

### For loop
```bash
for i in 1 2 3 4 5; do
  echo "Number $i"
done
```

### While loop
```bash
count=1
while [ $count -le 5 ]; do
  echo "Count $count"
  ((count++))
done
```

### Until loop
```bash
count=1
until [ $count -gt 5 ]; do
  echo "Count $count"
  ((count++))
done
```

### Break and Continue
```bash
for i in {1..10}; do
  if [ $i -eq 5 ]; then
    break
  fi
  echo $i
done
```

---

## 7. Functions
- Define:
  ```bash
  function greet() {
    echo "Hello, $1"
  }
  ```
- Call:
  ```bash
  greet "Bob"
  ```

- Return values (via exit codes):
  ```bash
  function is_even() {
    if (( $1 % 2 == 0 )); then
      return 0
    else
      return 1
    fi
  }

  is_even 4
  if [ $? -eq 0 ]; then
    echo "Even"
  else
    echo "Odd"
  fi
  ```

---

## 8. Command Line Arguments
- Access with `$1`, `$2`, etc. (`$0` is script name).
- `$@` = all arguments, `$#` = number of arguments.

Example:
```bash
echo "First argument: $1"
echo "Second argument: $2"
echo "Total arguments: $#"
```

Loop through all arguments:
```bash
for arg in "$@"; do
  echo "$arg"
done
```

---

## 9. Arrays
- Define an array:
  ```bash
  fruits=("apple" "banana" "cherry")
  ```
- Access:
  ```bash
  echo ${fruits[0]}
  ```
- All elements:
  ```bash
  echo ${fruits[@]}
  ```

- Loop:
  ```bash
  for fruit in "${fruits[@]}"; do
    echo "$fruit"
  done
  ```

---

## 10. String Manipulation
- Length:
  ```bash
  ${#string}
  ```

- Substring:
  ```bash
  ${string:position:length}
  ```

- Replace:
  ```bash
  ${string/old/new}
  ```

---

## 11. File Testing
```bash
if [ -f "$file" ]; then
  echo "File exists"
fi
```

### Common tests

| Test | Meaning |
|:---|:---|
| `-e` | File exists |
| `-d` | Is directory |
| `-f` | Is file |
| `-s` | Not empty |
| `-r` | Readable |
| `-w` | Writable |
| `-x` | Executable |

---

## 12. Redirection and Pipes
- Redirect output to a file:
  ```bash
  echo "Hello" > file.txt
  ```
- Append output:
  ```bash
  echo "Hello again" >> file.txt
  ```
- Redirect errors:
  ```bash
  command 2> error.log
  ```
- Pipe output to another command:
  ```bash
  ls -l | grep "Jan"
  ```

---

## 13. Important Special Variables

| Variable | Meaning |
|:---|:---|
| `$0` | Script name |
| `$1`..`$9` | First 9 arguments |
| `$@` | All arguments individually |
| `$*` | All arguments as single string |
| `$#` | Number of arguments |
| `$$` | Script PID |
| `$?` | Exit status of last command |

---

## 14. Exit Codes
- By convention:
  - `0` = success
  - Non-zero = failure
- Check:
  ```bash
  if [ $? -eq 0 ]; then
    echo "Success"
  else
    echo "Failure"
  fi
  ```

- Custom exit:
  ```bash
  exit 1
  ```

---

## 15. Trap and Signal Handling
- Trap signals like `CTRL+C`:
  ```bash
  trap "echo 'You pressed Ctrl+C!'; exit" SIGINT
  ```

---

## 16. Useful Bash Tools
- `sed` – Stream editor for filtering and transforming text.
- `awk` – Pattern scanning and processing language.
- `cut`, `sort`, `uniq`, `tr`, `grep`, `find`, `xargs`.

Example:
```bash
grep "something" file.txt | sort | uniq
```

---

## 17. Best Practices
- **Quote your variables** (`"$var"`) to prevent globbing and word splitting.
- **Use functions** to organize scripts.
- **Use meaningful variable names**.
- **Error handling** is important.
- **Comment your code** generously:
  ```bash
  # This loop prints numbers 1 to 5
  for i in {1..5}; do
    echo $i
  done
  ```

---

