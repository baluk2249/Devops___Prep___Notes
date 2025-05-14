# Linux Networking

Networking is a core component of Linux systems, used in server management, troubleshooting, and DevOps operations. This document outlines important concepts, tools, and commands for managing and troubleshooting Linux networking.

---

## 📡 Basic Concepts

* **IP Address**: Logical address for network identification.
* **Subnet Mask**: Defines network and host portions of the IP.
* **Gateway**: A node that routes traffic from one network to another.
* **DNS**: Resolves domain names to IP addresses.
* **MAC Address**: Unique hardware identifier for a network interface.

---

## 🔧 Viewing and Configuring Network Interfaces

### 1. `ip` Command (Preferred)

```bash
ip addr show
ip link show
ip route show
```

### 2. `ifconfig` (Legacy)

```bash
ifconfig
```

---

## 🌐 Checking Network Connectivity

### 1. `ping`

```bash
ping google.com
```

Sends ICMP packets to test reachability.

### 2. `traceroute` / `tracepath`

```bash
traceroute google.com
tracepath google.com
```

Traces the path packets take to a destination.

### 3. `curl` or `wget`

```bash
curl https://example.com
wget https://example.com
```

Tests application-level connectivity (HTTP/S).

### 4. `telnet` / `nc` (netcat)

```bash
telnet example.com 80
nc -zv example.com 80
```

Tests if a specific port is open.

---

## 📄 Viewing Routing Table

```bash
ip route
route -n
```

Displays the system's routing table.

---

## 🛠 DNS Configuration

### Check DNS Servers

```bash
cat /etc/resolv.conf
```

### Test DNS Resolution

```bash
nslookup example.com
dig example.com
```

---

## 📶 Network Interface Management

### Bring Interface Up/Down

```bash
ip link set eth0 up
ip link set eth0 down
```

### Assign IP Address

```bash
ip addr add 192.168.1.100/24 dev eth0
```

### Delete IP Address

```bash
ip addr del 192.168.1.100/24 dev eth0
```

---

## 🔐 Firewall and Port Control

### 1. `iptables` (Legacy)

```bash
iptables -L
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

### 2. `firewalld` (Modern)

```bash
firewall-cmd --list-all
firewall-cmd --add-port=80/tcp
```

### 3. `ufw` (User-friendly Firewall)

```bash
ufw enable
ufw allow 22/tcp
```

---

## 📈 Monitoring Tools

### 1. `netstat` (Deprecated in favor of `ss`)

```bash
netstat -tuln
```

### 2. `ss`

```bash
ss -tuln
ss -pant
```

### 3. `iftop` / `nethogs`

```bash
iftop
nethogs eth0
```

### 4. `tcpdump`

```bash
tcpdump -i eth0
```

Captures raw packet data from the network.

### 5. `iptraf-ng`

```bash
iptraf-ng
```

Text-based real-time network monitoring.

---

## 🧪 Example Scenario: Troubleshoot No Internet Access

### 1. Check interface status:

```bash
ip link show
```

### 2. Check IP address:

```bash
ip addr show
```

### 3. Check route:

```bash
ip route
```

### 4. Test DNS:

```bash
nslookup google.com
```

### 5. Ping external server:

```bash
ping 8.8.8.8
```

### 6. Check firewall rules:

```bash
sudo iptables -L
```

---

## ✅ Summary Table

| Task                 | Command                        |
| -------------------- | ------------------------------ |
| View IP & interfaces | `ip addr`, `ip link`           |
| Test connectivity    | `ping`, `traceroute`           |
| View routes          | `ip route`                     |
| DNS lookup           | `dig`, `nslookup`              |
| Open port check      | `nc`, `telnet`                 |
| Monitor traffic      | `iftop`, `tcpdump`             |
| Manage firewall      | `iptables`, `ufw`, `firewalld` |

---
