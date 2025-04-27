# 📜 `sed`

## 1. What is `sed`?

- **`sed`** stands for **Stream Editor**.
- It reads text line-by-line, applies operations, and outputs the result.
- Ideal for **substitutions**, **insertions**, **deletions**, and **transformations** on text files or streams.

---

## 2. Basic Syntax

```bash
sed [options] 'command' file
```

- `command` tells `sed` what to do.
- You can also chain multiple commands.

Example:

```bash
sed 's/old/new/' file.txt
```

> Replaces first occurrence of "old" with "new" in each line.

---

## 3. Basic Operations

### Substitution (Find and Replace)

```bash
sed 's/old/new/' file.txt
```

- `s` → substitute
- `old` → pattern to find
- `new` → replacement

### Replace Globally in a Line

```bash
sed 's/old/new/g' file.txt
```

> `g` flag replaces **all** occurrences in a line.

### Case-Insensitive Replace

```bash
sed 's/old/new/gi' file.txt
```

> `i` flag makes it **case-insensitive**.

---

## 4. Addressing (Target Specific Lines)

### Replace in a Specific Line

```bash
sed '2s/old/new/' file.txt
```

> Only changes in line 2.

### Replace Between Line Ranges

```bash
sed '2,5s/old/new/' file.txt
```

> Changes between lines 2 and 5.

### Replace Only in Matching Lines

```bash
sed '/pattern/s/old/new/' file.txt
```

> Changes only in lines that match "pattern".

---

## 5. Deleting Lines

### Delete Specific Line

```bash
sed '3d' file.txt
```

> Deletes line 3.

### Delete Range of Lines

```bash
sed '5,10d' file.txt
```

> Deletes lines 5 through 10.

### Delete Matching Lines

```bash
sed '/pattern/d' file.txt
```

> Deletes lines containing "pattern".

---

## 6. Inserting and Appending Text

### Insert Before a Line

```bash
sed '3i\Inserted line' file.txt
```

> Inserts text **before** line 3.

### Append After a Line

```bash
sed '3a\Appended line' file.txt
```

> Appends text **after** line 3.

### Change (Replace) a Line

```bash
sed '3c\This is the new line' file.txt
```

> Replaces line 3 entirely.

---

## 7. Print Specific Lines

### Print Line 5

```bash
sed -n '5p' file.txt
```

> `-n` suppresses automatic printing.

### Print Lines Matching a Pattern

```bash
sed -n '/pattern/p' file.txt
```

### Print Line Ranges

```bash
sed -n '2,5p' file.txt
```

---

## 8. Using Multiple Commands

### Using `-e`

```bash
sed -e 's/old1/new1/' -e 's/old2/new2/' file.txt
```

### Using `{}` Grouping

```bash
sed '/pattern/{s/old/new/; s/foo/bar/}' file.txt
```

> Apply multiple operations on matching lines.

---

## 9. Saving Changes In-place

### Edit File Directly

```bash
sed -i 's/old/new/g' file.txt
```

> `-i` edits the file **in-place**.

### Create a Backup

```bash
sed -i.bak 's/old/new/g' file.txt
```

> Creates a backup `file.txt.bak` before editing.

---

## 10. Special Characters Handling

### Escape Special Characters

```bash
sed 's/\/\\/g' file.txt
```

> Double escape backslashes.

### Different Delimiters

```bash
sed 's|/usr/bin|/bin|' file.txt
```

> Use `|` as delimiter instead of `/`.

---

## 11. Regular Expressions

### Basic Regex

- `.` → any single character
- `*` → zero or more repetitions
- `^` → start of line
- `$` → end of line
- `[]` → character class

Example:

```bash
sed -n '/^[a-z]/p' file.txt
```

> Lines starting with a lowercase letter.

### Extended Regex (with `-E`)

```bash
sed -E 's/(foo|bar)/baz/' file.txt
```

> Matches `foo` or `bar` and replaces with `baz`.

---

## 12. Advanced Techniques

### Remove Blank Lines

```bash
sed '/^$/d' file.txt
```

### Replace Tabs with Spaces

```bash
sed 's/\t/    /g' file.txt
```

### Remove Trailing Whitespaces

```bash
sed 's/[[:space:]]*$//' file.txt
```

### Insert Line Number

```bash
sed = file.txt | sed 'N;s/\n/ /'
```

---

## 13. Useful One-Liners

| Task                           | `sed` Command                                                         |
| ------------------------------ | --------------------------------------------------------------------- |
| Replace word                   | `sed 's/old/new/' file`                                               |
| Delete blank lines             | `sed '/^$/d' file`                                                    |
| Remove first line              | `sed '1d' file`                                                       |
| Add text after a pattern       | `sed '/pattern/a\New Text' file`                                      |
| Convert lowercase to uppercase | `sed 'y/abcdefghijklmnopqrstuvwxyz/ABCDEFGHIJKLMNOPQRSTUVWXYZ/' file` |

---

# 🔥 Pro Tip:

> Combine `sed` with `grep`, `awk`, `cut`, and `sort` for **advanced pipelines**!

Example:

```bash
grep 'error' logfile | sed 's/error/ERROR/g' | sort | uniq
```

---

