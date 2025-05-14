# `lsof`

## Overview

`lsof` (List Open Files) is a powerful command-line utility in Unix/Linux used to report a list of all open files and the processes that opened them. In Unix, everything is a file—including network connections and devices—so `lsof` can be used to examine open ports, files, directories, libraries, and sockets.

---

## Basic Syntax

```bash
lsof [options] [names]
```

---

## Commonly Used Options

| Option      | Description                                              |
| ----------- | -------------------------------------------------------- |
| `-i`        | Show network files (IP sockets)                          |
| `-u [user]` | Show files opened by a specific user                     |
| `-p [PID]`  | Show files opened by a specific process ID               |
| `-c [name]` | Show files opened by processes matching the name         |
| `-n`        | No DNS name resolution                                   |
| `-P`        | Show port numbers instead of service names               |
| `+d [dir]`  | Show files under the specified directory                 |
| `+D [dir]`  | Recursively list all files under the specified directory |

---

## Example Usages

### 1. List All Open Files

```bash
lsof
```

### 2. List Open Files for a Specific User

```bash
lsof -u username
```

### 3. Show Network Connections

```bash
lsof -i
```

### 4. Show Listening TCP Ports

```bash
lsof -iTCP -sTCP:LISTEN
```

### 5. Find the Process Using a Specific Port (e.g., 8080)

```bash
lsof -i :8080
```

### 6. Show Files Opened by a Specific Process ID

```bash
lsof -p 1234
```

### 7. List Files Opened by a Specific Program Name (e.g., sshd)

```bash
lsof -c sshd
```

### 8. List Open Files in a Specific Directory

```bash
lsof +D /var/log
```

---

## Output Explanation

| Column     | Description                               |
| ---------- | ----------------------------------------- |
| `COMMAND`  | Name of the command/process               |
| `PID`      | Process ID                                |
| `USER`     | User owning the process                   |
| `FD`       | File descriptor (e.g., cwd, txt, mem, 1u) |
| `TYPE`     | Type of node (e.g., REG, DIR, IPv4)       |
| `DEVICE`   | Device numbers                            |
| `SIZE/OFF` | Size or offset                            |
| `NODE`     | Node number (inode)                       |
| `NAME`     | Name of the file or mount point           |

#### Common File Descriptors (FD)

| FD    | Meaning                         |
| ----- | ------------------------------- |
| `cwd` | Current working directory       |
| `txt` | Program text (code and data)    |
| `mem` | Memory-mapped file              |
| `0u`  | Standard input (u = read/write) |
| `1u`  | Standard output                 |
| `2u`  | Standard error                  |

---

## Tips for Effective Use

* Combine `-nP` to speed up network scans and avoid DNS/port resolution:

  ```bash
  lsof -i -nP
  ```
* Pipe output to `grep` to search for specific terms:

  ```bash
  lsof -i | grep ssh
  ```
* Use `lsof` to check which processes have a file open before unmounting a filesystem:

  ```bash
  lsof +D /mnt/usb
  ```

---

## Security and Troubleshooting Use Cases

* **Find open ports and associated programs**
* **Detect malicious activity (e.g., suspicious open ports or connections)**
* **Identify file descriptor leaks in long-running processes**
* **Trace locked files**
* **Monitor file access in critical directories**

---

