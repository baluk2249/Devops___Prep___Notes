# `netstat`

## Overview

`netstat` (network statistics) is a command-line tool used for monitoring network connections, routing tables, interface statistics, masquerade connections, and multicast memberships. It is helpful in diagnosing network issues and understanding network performance.

> Note: On modern Linux systems, `ss` is the recommended replacement for `netstat` as it's faster and provides more detailed information.

---

## Basic Syntax

```bash
netstat [options]
```

---

## Commonly Used Options

| Option | Description                                              |
| ------ | -------------------------------------------------------- |
| `-a`   | Show all connections (listening and non-listening)       |
| `-t`   | Display TCP connections                                  |
| `-u`   | Display UDP connections                                  |
| `-n`   | Show numerical addresses instead of resolving hostnames  |
| `-l`   | Show only listening sockets                              |
| `-p`   | Show process ID and name of the program using the socket |
| `-r`   | Display routing table                                    |
| `-i`   | Show network interface statistics                        |
| `-s`   | Show summary statistics for each protocol                |

---

## Example Usages

### 1. Show All Connections (Listening and Established)

```bash
netstat -a
```

### 2. Show Only Listening TCP Ports

```bash
netstat -lt
```

### 3. Show Active UDP Connections

```bash
netstat -u
```

### 4. Show Routing Table

```bash
netstat -r
```

### 5. Show Interface Statistics

```bash
netstat -i
```

### 6. Show Network Connections with Process Information

```bash
sudo netstat -tunlp
```

* `-t`: TCP
* `-u`: UDP
* `-n`: No DNS resolution
* `-l`: Listening sockets
* `-p`: Show PID/program

### 7. Display Protocol Statistics

```bash
netstat -s
```

---

## Output Explanation

### TCP/UDP Connection Output

| Column             | Description                                  |
| ------------------ | -------------------------------------------- |
| `Proto`            | Protocol used (TCP/UDP)                      |
| `Recv-Q`           | Bytes received and queued                    |
| `Send-Q`           | Bytes to be sent                             |
| `Local Address`    | Local IP and port                            |
| `Foreign Address`  | Remote IP and port                           |
| `State`            | Connection state (e.g., LISTEN, ESTABLISHED) |
| `PID/Program name` | Process using the socket (if `-p` used)      |

---

## Connection States (TCP)

| State         | Meaning                                         |
| ------------- | ----------------------------------------------- |
| `LISTEN`      | Waiting for incoming connections                |
| `ESTABLISHED` | Connection is open and data can be sent         |
| `CLOSE_WAIT`  | Remote side has closed; waiting for local close |
| `TIME_WAIT`   | Waiting after closing to handle late packets    |
| `SYN_SENT`    | Client sent SYN; waiting for SYN-ACK            |
| `SYN_RECV`    | Server received SYN; waiting for ACK            |

---

## Interpretation Tips

* High number of `TIME_WAIT` states is normal for busy servers.
* `CLOSE_WAIT` that persists may indicate an application not closing connections properly.
* Use `netstat -an | grep :80` to monitor traffic on a specific port (e.g., HTTP).

---

