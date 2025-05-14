# Memory Leaks

Memory leaks in production environments can lead to performance degradation, crashes, and system outages. As a DevOps engineer, you should be equipped to detect, analyze, and resolve memory leaks efficiently.

---

## 🔍 What is a Memory Leak?

A memory leak occurs when an application consumes memory but fails to release it back to the system. Over time, this leads to a depletion of available memory.

---

## 🧩 Common Causes

* Improper memory deallocation in code (C/C++)
* Persistent data structures in interpreted languages (Python, Node.js, Java)
* Poorly scoped variables in long-running processes
* Resource leaks in services like Apache, Nginx, or custom apps

---

## 📋 Symptoms of a Memory Leak

* Gradual increase in memory usage
* Sluggish system or service performance
* Frequent Out-Of-Memory (OOM) kills
* Application or container crashes

---

## 🚦 Step-by-Step Troubleshooting

### 1. **Initial Memory Check**

```bash
free -h
```

Shows used, free, and cached memory.

### 2. **Identify Memory Hogs**

```bash
ps aux --sort=-%mem | head
```

Lists top processes by memory usage.

### 3. **Use `top` or `htop` for Live Monitoring**

```bash
top
```

or

```bash
htop
```

Observe if memory usage grows over time.

### 4. **Track Memory Growth Over Time**

```bash
watch -n 5 "ps -eo pid,pmem,pcpu,comm --sort=-pmem | head"
```

### 5. **Detailed Analysis with `smem`**

```bash
smem -r | sort -k 4 -nr | head
```

Gives shared/private/proportional memory usage per process.

### 6. **Memory Mapping with `pmap`**

```bash
pmap -x <PID> | less
```

Helps understand how a process allocates memory.

---

## 🧪 Development/Debug Tools

### 🧠 `valgrind` (Native Binaries)

```bash
valgrind --leak-check=full ./your_binary
```

Detects and reports leaked memory locations.

### 📊 `massif` (Heap Profiler via Valgrind)

```bash
valgrind --tool=massif ./your_binary
ms_print massif.out.<pid>
```

Visualizes heap usage.

### 🔥 `gperftools` / `heaptrack` / `jemalloc`

* Good for performance and memory leak profiling in C/C++
* Tools like `heaptrack` allow tracing memory allocations with stack traces

### 🐍 Python: `objgraph`, `tracemalloc`

```python
import tracemalloc
tracemalloc.start()
```

Tracks memory allocations and differences

### ☕ Java: `jmap`, `jvisualvm`, `MAT (Memory Analyzer Tool)`

```bash
jmap -dump:format=b,file=heapdump.hprof <pid>
```

Analyze using VisualVM or Eclipse MAT.

### 🟢 Node.js: `clinic.js`, `heapdump`, Chrome DevTools

```js
require('heapdump').writeSnapshot('snapshot.heapsnapshot');
```

Analyze `.heapsnapshot` in Chrome DevTools.

---

## 🧰 In-Production Monitoring Tools

* **Prometheus + Grafana**: Track memory usage over time.
* **Datadog**, **New Relic**, **AppDynamics**: Alerts and dashboards for memory trends.
* **cAdvisor**: Monitor container memory usage in Kubernetes.

---

## 🛡️ Prevention Tips

* Use memory-safe languages (Go, Rust) when possible
* Apply load testing tools (Locust, JMeter, k6) to simulate usage patterns
* Write unit/integration tests that include memory profiling
* Regularly restart services prone to leaking (if no fix is available)

---

## ✅ Summary

| Step | Tool/Command            | Purpose                         |
| ---- | ----------------------- | ------------------------------- |
| 1    | `free`, `top`, `ps`     | Get memory overview             |
| 2    | `smem`, `pmap`          | Process memory breakdown        |
| 3    | `valgrind`, `massif`    | Analyze C/C++ code leaks        |
| 4    | Language-specific tools | For Python, Java, Node.js, etc. |
| 5    | Monitoring dashboards   | Detect trends in production     |

---

