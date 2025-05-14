## `iostat` (Input/Output Statistics)

`iostat` is part of the `sysstat` package and provides detailed reports on CPU usage and I/O statistics for devices, partitions, and system-wide operations. It's commonly used to identify I/O bottlenecks and monitor disk performance.

---

### Basic Syntax

```bash
iostat [options] [delay [count]]
```

* **`delay`**: Interval (in seconds) between reports
* **`count`**: Number of reports to generate

#### Example:

```bash
iostat -xz 2 5
```

Detailed extended stats every 2 seconds, repeated 5 times.

---

### Key Output Sections

#### 1. CPU Statistics

| Column    | Description                                 |
| --------- | ------------------------------------------- |
| `%user`   | Time spent on user processes                |
| `%nice`   | Time spent on low-priority (nice) processes |
| `%system` | Time spent on kernel processes              |
| `%iowait` | Time CPU waits for I/O completion           |
| `%steal`  | Time stolen by hypervisor (VMs)             |
| `%idle`   | Idle CPU time                               |

#### 2. Device Statistics

| Column      | Description                           |
| ----------- | ------------------------------------- |
| `Device`    | Device name (e.g., sda, nvme0n1)      |
| `tps`       | Transfers per second (I/O operations) |
| `kB_read/s` | Kilobytes read per second             |
| `kB_wrtn/s` | Kilobytes written per second          |
| `kB_read`   | Total KB read                         |
| `kB_wrtn`   | Total KB written                      |

#### 3. Extended Statistics (with `-x` option)

| Column     | Description                                    |
| ---------- | ---------------------------------------------- |
| `rrqm/s`   | Read requests merged per second                |
| `wrqm/s`   | Write requests merged per second               |
| `r/s`      | Read requests per second                       |
| `w/s`      | Write requests per second                      |
| `rsec/s`   | Sectors read per second                        |
| `wsec/s`   | Sectors written per second                     |
| `avgrq-sz` | Average request size (in sectors)              |
| `avgqu-sz` | Average queue length of I/O requests           |
| `await`    | Average time (ms) for I/O request completion   |
| `svctm`    | Average service time (deprecated, use `await`) |
| `%util`    | Percentage of time device was busy             |

> **Note**: High `%util` near 100% and high `await` suggest disk saturation.

---

### Useful Options

| Option | Description                                                |
| ------ | ---------------------------------------------------------- |
| `-x`   | Extended statistics (recommended for performance analysis) |
| `-d`   | Only display device stats                                  |
| `-m`   | Display in megabytes instead of kilobytes                  |
| `-k`   | Force output in kilobytes (default)                        |
| `-p`   | Include partition statistics                               |
| `-z`   | Suppress devices with zero activity                        |

---

### Interpretation Tips

* **High `%iowait`** → Possible I/O bottleneck
* **High `await`** → Slow device response time
* **High `%util`** (near 100%) → Disk is saturated
* **High `avgqu-sz`** → Long queues; potential throughput issues

---

### Common Use Cases

* Monitor disk performance trends over time
* Identify slow or overloaded storage devices
* Track I/O load distribution across devices
* Diagnose latency issues in I/O-intensive applications

---

