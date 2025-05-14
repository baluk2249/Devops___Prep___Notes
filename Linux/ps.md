# `ps`

## Overview

`ps` (process status) is a command-line utility used to display information about active processes on a Unix/Linux system. It can show process IDs (PIDs), memory and CPU usage, user ownership, execution time, and more. It is a vital tool for process monitoring and system troubleshooting.

---

## Basic Syntax

```bash
ps [options]
```

---

## Commonly Used Options

| Option        | Description                                                |
| ------------- | ---------------------------------------------------------- |
| `-e` or `-A`  | Show all processes                                         |
| `-f`          | Full-format listing (includes UID, PPID, start time, etc.) |
| `-u [user]`   | Show processes for a specific user                         |
| `-p [pid]`    | Show a specific process by PID                             |
| `-o [format]` | Specify custom output format                               |
| `-x`          | Include processes without a terminal                       |
| `aux`         | Show all processes in BSD style                            |

---

## Common Formats and Flags

### 1. Show All Processes (Standard Format)

```bash
ps -e
```

### 2. Show All Processes (Full Format)

```bash
ps -ef
```

### 3. Show All Processes in BSD Style

```bash
ps aux
```

### 4. Show Processes for a Specific User

```bash
ps -u username
```

### 5. Show Specific PID

```bash
ps -p 1234
```

### 6. Custom Output Format

```bash
ps -eo pid,ppid,cmd,%mem,%cpu
```

---

## Output Column Explanation (Standard `ps -ef`)

| Column  | Description                          |
| ------- | ------------------------------------ |
| `UID`   | User ID of the process owner         |
| `PID`   | Process ID                           |
| `PPID`  | Parent Process ID                    |
| `C`     | CPU utilization                      |
| `STIME` | Start time of the process            |
| `TTY`   | Terminal associated with the process |
| `TIME`  | Total CPU time used by the process   |
| `CMD`   | Command used to start the process    |

---

## Filtering and Grep Examples

### Find All Running Instances of a Process (e.g., nginx)

```bash
ps aux | grep nginx
```

### Exclude `grep` from Output

```bash
ps aux | grep '[n]ginx'
```

---

## Real-Time Monitoring

`ps` is often used with tools like `watch` to create real-time monitoring:

```bash
watch -n 2 'ps -eo pid,cmd,%mem,%cpu --sort=-%mem | head'
```

This command refreshes every 2 seconds and shows the top memory-consuming processes.

---

## Use Cases

* Identify high resource-consuming processes
* Find zombie or defunct processes
* Trace process hierarchy and parent-child relationships
* Debug orphan or runaway processes
* Monitor background daemons and cron jobs

---

