`vmstat` (Virtual Memory Statistics) is a performance monitoring tool available on Unix/Linux systems. It provides real-time reporting of various system metrics such as processes, memory, paging, block I/O, traps, and CPU activity.

---

## Basic Syntax

```bash
vmstat [options] [delay [count]]
```

* **`delay`**: Interval in seconds between updates.
* **`count`**: Number of updates to display.
* **No arguments**: Displays average statistics since the last reboot.

### Example:

```bash
vmstat 2 5
```

Reports statistics every 2 seconds, for 5 intervals.

---

## Output Fields Explained

### 1. Procs (Processes)

| Column | Description                                           |
| ------ | ----------------------------------------------------- |
| `r`    | Runnable processes (ready to run)                     |
| `b`    | Processes in uninterruptible sleep (usually I/O wait) |

### 2. Memory

| Column  | Description                             |
| ------- | --------------------------------------- |
| `swpd`  | Virtual memory used (swap), in KB       |
| `free`  | Idle memory, in KB                      |
| `buff`  | Memory used as buffers for raw disk I/O |
| `cache` | Memory used to cache file data          |

### 3. Swap

| Column | Description                                   |
| ------ | --------------------------------------------- |
| `si`   | Memory swapped in from disk per second (KB/s) |
| `so`   | Memory swapped out to disk per second (KB/s)  |

### 4. IO (Block Input/Output)

| Column | Description                                            |
| ------ | ------------------------------------------------------ |
| `bi`   | Blocks received from a block device (read), per second |
| `bo`   | Blocks sent to a block device (write), per second      |

### 5. System

| Column | Description                            |
| ------ | -------------------------------------- |
| `in`   | Interrupts per second, including clock |
| `cs`   | Context switches per second            |

### 6. CPU

All values are percentages of total CPU time.

| Column | Description                             |
| ------ | --------------------------------------- |
| `us`   | Time spent on user processes            |
| `sy`   | Time spent on system (kernel) processes |
| `id`   | Idle time                               |
| `wa`   | Time waiting for I/O                    |
| `st`   | Time stolen from VM by hypervisor       |

---

## Useful Options

| Option           | Description                                          |
| ---------------- | ---------------------------------------------------- |
| `-a`             | Show active/inactive memory                          |
| `-s`             | Display event counters and memory stats summary      |
| `-m`             | Show slabinfo (kernel memory usage)                  |
| `-d`             | Display disk statistics                              |
| `-p [partition]` | Report stats for a specific partition                |
| `-S [unit]`      | Set output units: k (kilobytes), m (megabytes), etc. |

---

## Performance Interpretation Tips

* **`r` > number of CPUs** → Possible CPU bottleneck.
* **High `wa`** → Indicates I/O bottleneck.
* **High `so` / `si`** → Excessive swapping; memory pressure.
* **High `cs`** → Many context switches; possible inefficient process handling.

---

## Common Use Cases

* Diagnosing system performance bottlenecks
* Monitoring memory and swap usage
* Real-time performance tracking during testing or troubleshooting
* Correlating CPU wait and system load during I/O-intensive operations

---

