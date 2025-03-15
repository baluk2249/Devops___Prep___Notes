# Linux `find` Command Examples

## 📂 Example Directory Structure
Assume we have the following directory and file structure:

```
/var/www
├── logs
│   ├── app.log
│   ├── error.log
│   ├── access.log
├── backups
│   ├── db_backup.sql
│   ├── files_backup.tar.gz
├── scripts
│   ├── deploy.sh
│   ├── cleanup.sh
│   ├── monitor.sh
├── uploads
│   ├── image1.jpg
│   ├── document.pdf
│   ├── report.docx
```

---

## 🛠 Setting Up the Example Environment

### 🔹 Clone the Repository
To try out these examples, clone the repository containing the necessary files:

```bash
git clone https://github.com/example/find-command-examples.git
cd Linux_Devops_Handson/Linux/find/
```


---

## 🛠 Basic `find` Commands

### 1. Find All Files and Directories
```bash
find var/www
```

### 2. Find Files by Name
```bash
find var/www -name "app.log"
```

#### Case-Insensitive Search
```bash
find var/www -iname "APP.LOG"
```

### 3. Find Directories by Name
```bash
find var/www -type d -name "logs"
```

### 4. Find Only Files
```bash
find var/www -type f
```

### 5. Find Only Directories
```bash
find var/www -type d
```

### 6. Find Files by Extension
```bash
find var/www -type f -name "*.sh"
```

### 7. Find Files by Size
#### Find files larger than 100MB
```bash
find var/www -type f -size +100M
```

#### Find files smaller than 1KB
```bash
find var/www -type f -size -1k
```

### 8. Find Files by Permissions
#### Find files with 777 permissions
```bash
find var/www -type f -perm 777
```

#### Find executable files
```bash
find var/www -type f -executable
```

### 9. Find Files by Modification Time
#### Find files modified in the last 7 days
```bash
find var/www -type f -mtime -7
```

#### Find files modified more than 30 days ago
```bash
find var/www -type f -mtime +30
```

### 10. Find Empty Files and Directories
#### Find empty files
```bash
find var/www -type f -empty
```

#### Find empty directories
```bash
find var/www -type d -empty
```

### 11. Find Files and Delete Them
#### Delete `.log` files older than 30 days
```bash
find var/www -type f -name "*.log" -mtime +30 -delete
```

### 12. Find and Execute Commands
#### Find `.sh` files and list details
```bash
find var/www -type f -name "*.sh" -exec ls -l {} \;
```

#### Find and change permissions
```bash
find var/www -type f -name "*.sh" -exec chmod +x {} \;
```

---

## 🔥 Advanced `find` Examples

### 13. Find Files Using `-depth`
#### Find files, processing directories last
```bash
find var/www -depth -type f
```

### 14. Using `-exec {} +` for Efficiency
#### List all `.sh` files (faster than `-exec {} \;`)
```bash
find var/www -type f -name "*.sh" -exec ls -l {} +
```

### 15. Using `-printf` for Custom Output
#### Print filenames with their sizes in human-readable format
```bash
find var/www -type f -printf "%p %k KB\n"
```

### 16. Using Logical Operators (`-or`, `-and`, `!`)
#### Find `.sh` OR `.log` files
```bash
find var/www -type f \( -name "*.sh" -or -name "*.log" \)
```

#### Find files that are NOT `.jpg`
```bash
find var/www -type f ! -name "*.jpg"
```

### 17. Find and Move Files
#### Move `.log` files to another directory
```bash
find var/www -type f -name "*.log" -exec mv {} /var/www/archived_logs/ \;
```

### 18. Find and Archive Files
#### Find all `.log` files and compress them
```bash
find var/www -type f -name "*.log" | tar -czvf logs_backup.tar.gz -T -
```

### 19. Find Symbolic Links
```bash
find var/www -type l
```

---

These examples cover simple to advanced `find` usage in Linux. 🚀

