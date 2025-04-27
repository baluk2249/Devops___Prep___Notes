# 📜 Mastering `awk`: Detailed Notes

## 1. What is `awk`?
- **`awk`** is a powerful **text-processing** language.
- Named after its creators: **A**ho, **W**einberger, and **K**ernighan.
- It operates on a **line-by-line** basis and **splits lines into fields**.
- Great for **data extraction**, **report generation**, and **simple data manipulation**.

---

## 2. Basic Syntax
```bash
awk 'pattern {action}' file
```
- **pattern** → condition to match (optional).
- **action** → what to do if pattern matches.
- If pattern is omitted, action is applied to all lines.

Example:
```bash
awk '{print $1}' file.txt
```
> Prints the first word (field) from each line.

---

## 3. Important Concepts
- `awk` reads **one line at a time**.
- It **splits each line into fields** using a delimiter (default = space/tab).
- **Fields**: `$1`, `$2`, ..., `$NF`
  - `$0` → whole line
  - `$1` → first field
  - `$2` → second field
  - `$NF` → last field (NF = Number of Fields)

---

## 4. Common Usage

### Print Specific Columns
```bash
awk '{print $1, $3}' file.txt
```
> Prints 1st and 3rd fields.

---

### Search for Specific Lines
```bash
awk '/pattern/ {print $0}' file.txt
```
> Prints lines that match "pattern".

---

### Change Field Separator
```bash
awk -F: '{print $1, $3}' /etc/passwd
```
> `-F` sets the **input field separator** (here, colon `:`).

---

### Specify Output Separator
```bash
awk 'BEGIN {OFS=" - " } {print $1, $2}' file.txt
```
> Sets **Output Field Separator** to ` - `.

---

## 5. BEGIN and END Blocks
- **`BEGIN`** → run before processing any line.
- **`END`** → run after processing all lines.

Example:
```bash
awk 'BEGIN {print "Start"} {print $1} END {print "End"}' file.txt
```
> Prints "Start" first, processes all lines, then prints "End".

---

## 6. Variables in `awk`

- **Built-in variables**:
  - `NR` → Number of Records (lines)
  - `NF` → Number of Fields in current line
  - `FS` → Field Separator
  - `OFS` → Output Field Separator
  - `RS` → Record Separator (default: newline)

Example:
```bash
awk '{print NR, NF, $0}' file.txt
```
> Prints line number, number of fields, and the line.

- **User-defined variables**:
```bash
awk '{x = $2 * 2; print x}' file.txt
```
> Multiplies second field by 2 and prints it.

---

## 7. Conditional Statements
```bash
awk '{if ($2 > 50) print $1, $2}' file.txt
```
> Prints lines where second field > 50.

You can also use `else`, `else if`:
```bash
awk '{
  if ($2 > 80) print $1, "A"
  else if ($2 > 50) print $1, "B"
  else print $1, "C"
}' file.txt
```

---

## 8. Looping in `awk`

### For loop
```bash
awk '{for(i=1; i<=NF; i++) print $i}' file.txt
```
> Prints all fields one by one.

### While loop
```bash
awk '{i=1; while(i<=NF) {print $i; i++}}' file.txt
```

---

## 9. Functions in `awk`
- Define and use functions inside an awk script.

Example:
```bash
awk '
function square(x) { return x * x }
{ print $1, square($2) }
' file.txt
```
> Defines a `square` function and uses it.

---

## 10. String Operations
- `length($0)` → length of line
- `substr(string, start, length)` → substring
- `index(string, substring)` → position of substring
- `tolower(string)`, `toupper(string)`

Example:
```bash
awk '{print toupper($1)}' file.txt
```
> Converts the first field to uppercase.

---

## 11. Arrays in `awk`
- `awk` supports **associative arrays** (like dictionaries).

Example:
```bash
awk '{count[$1]++} END {for (word in count) print word, count[word]}' file.txt
```
> Counts frequency of first field (word count).

---

## 12. Regular Expressions
- Very powerful in pattern matching.

Examples:
```bash
awk '/^a/' file.txt
```
> Lines starting with "a".

```bash
awk '/[0-9]{3}/' file.txt
```
> Lines containing a three-digit number.

---

## 13. Advanced Awk Tricks

### Multiple Actions
```bash
awk '{print $1; print $2}' file.txt
```

### Match multiple patterns
```bash
awk '$1 == "error" || $2 > 100' file.txt
```

### In-line Arithmetic
```bash
awk '{print $1, $2*1.5}' file.txt
```

---

## 14. Writing `awk` Scripts (File)
You can write a standalone awk script:

**myscript.awk**
```awk
#!/usr/bin/awk -f
BEGIN {print "Starting..."}
{
  print $1, $NF
}
END {print "Done!"}
```

Make it executable:
```bash
chmod +x myscript.awk
./myscript.awk file.txt
```

---

## 15. Useful One-Liners

| Task | `awk` Command |
|:----|:--------------|
| Print first column | `awk '{print $1}' file` |
| Sum a column | `awk '{sum += $2} END {print sum}' file` |
| Average a column | `awk '{sum += $2; count++} END {print sum/count}' file` |
| Print lines > 5 fields | `awk 'NF > 5' file` |
| Swap two columns | `awk '{print $2, $1}' file` |

---

# 🔥 Pro Tip:
> Combine `awk` with `grep`, `sed`, `sort`, and `xargs` to perform **powerful text-processing pipelines**!

Example:
```bash
grep "error" log.txt | awk '{print $1, $2}' | sort | uniq -c
```

