# 📘 `grep` – Global Regular Expression Print

The `grep` command is used in Unix/Linux to **search for patterns** within text files. It uses **regular expressions** to match patterns and is **case-sensitive by default**.

---

## 🔹 Basic Syntax

```bash
grep [OPTIONS] PATTERN [FILE...]
```

---

## 📖 Common Options

| Option         | Description                                         |
| -------------- | --------------------------------------------------- |
| `-i`           | Ignore case (case-insensitive match)                |
| `-v`           | Invert match (show lines that do **not** match)     |
| `-r` / `-R`    | Recursively search directories                      |
| `-n`           | Show line numbers                                   |
| `-c`           | Show count of matching lines                        |
| `-l`           | Show file names with matches                        |
| `-L`           | Show file names **without** matches                 |
| `-o`           | Show only the matching part of the line             |
| `-w`           | Match **whole words** only                          |
| `-x`           | Match **entire lines** only                         |
| `-E`           | Use **extended regular expressions** (like `egrep`) |
| `-F`           | Interpret pattern as a **fixed string**, not regex  |
| `--color=auto` | Highlight matching patterns                         |

---

## 📈 Examples

### 1. **Search a word in a file**

```bash
grep "error" logfile.txt
```

### 2. **Case-insensitive search**

```bash
grep -i "error" logfile.txt
```

### 3. **Show line numbers with matches**

```bash
grep -n "timeout" server.log
```

### 4. **Count number of matches**

```bash
grep -c "200 OK" access.log
```

### 5. **Invert match (exclude lines)**

```bash
grep -v "DEBUG" app.log
```

### 6. **Show only matched text**

```bash
grep -o "http[^"]*" urls.txt
```

### 7. **Match whole word only**

```bash
grep -w "fail" results.txt
```

### 8. **Match full line**

```bash
grep -x "SUCCESS" output.log
```

### 9. **Search recursively in directory**

```bash
grep -r "password" /etc/
```

### 10. **Search multiple patterns using extended regex**

```bash
grep -E "error|fail|critical" log.txt
```

### 11. **Search using a pattern file**

```bash
grep -f patterns.txt file.txt
```

### 12. **Highlight matches**

```bash
grep --color=auto "disk" df.txt
```

### 13. **Find files that contain a pattern**

```bash
grep -l "api_key" *.env
```

### 14. **Find files that do NOT contain a pattern**

```bash
grep -L "api_key" *.env
```

### 15. **With pipelines**

```bash
ps aux | grep "nginx"
```

---

## 📚 grep vs egrep vs fgrep

| Tool                 | Description                                   |                     |
| -------------------- | --------------------------------------------- | ------------------- |
| `grep`               | Basic regular expressions                     |                     |
| `egrep` or `grep -E` | Extended regex (e.g., `+`, \`                 | `, `()\` supported) |
| `fgrep` or `grep -F` | Fixed string search (no regex interpretation) |                     |

---

## 🧠 Tips

* Use `grep -r pattern .` to search inside codebases.
* Use `grep -o` with `wc -l` to count word occurrences.

  ```bash
  grep -o -w "error" log.txt | wc -l
  ```
* Combine with `sort`, `uniq` to find most common lines:

  ```bash
  grep "failed" logs.txt | sort | uniq -c | sort -nr
  ```

---

## 🔧 Scripting Example

```bash
#!/bin/bash
read -p "Enter word to search: " word
grep -r -n --color=auto "$word" .
```
