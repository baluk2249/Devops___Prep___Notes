# IP & Subnets

## 📁 What is an IP Address?

An **IP address (Internet Protocol address)** is a unique identifier assigned to each device connected to a network that uses the Internet Protocol for communication. It serves two primary functions:

1. **Identification** – Identifies a host on a network.
2. **Location Addressing** – Provides the host's location in the network.

---

## 👤 Types of IP Addresses

### ✉ By Assignment:

* **Dynamic IP** – Assigned by DHCP servers; may change over time.
* **Static IP** – Manually configured and doesn't change.

### ⚖ By Accessibility:

* **Private IP** – Used within private networks; not routable on the internet.
* **Public IP** – Assigned to devices accessible over the internet.

---

## 📅 IPv4 vs IPv6

### 📊 IPv4

* 32-bit address
* Written as 4 octets separated by dots (e.g., `192.168.1.1`)
* \~4.3 billion possible addresses

### 🔢 IPv6

* 128-bit address
* Written in hexadecimal, separated by colons (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`)
* Vastly more addresses (\~340 undecillion)
* Includes features like auto-configuration, built-in security

---

## 🔹 Common IPv4 Classes

| Class | Range                       | Default Subnet Mask | Usage                 |
| ----- | --------------------------- | ------------------- | --------------------- |
| A     | 1.0.0.0 - 126.255.255.255   | 255.0.0.0           | Very large networks   |
| B     | 128.0.0.0 - 191.255.255.255 | 255.255.0.0         | Medium-sized networks |
| C     | 192.0.0.0 - 223.255.255.255 | 255.255.255.0       | Small networks        |
| D     | 224.0.0.0 - 239.255.255.255 | -                   | Multicast             |
| E     | 240.0.0.0 - 255.255.255.255 | -                   | Experimental          |

---

## 🏠 Private IP Ranges (RFC 1918)

* Class A: `10.0.0.0 – 10.255.255.255`
* Class B: `172.16.0.0 – 172.31.255.255`
* Class C: `192.168.0.0 – 192.168.255.255`

---

## 🔗 Loopback and Special Addresses

* `127.0.0.1` – Loopback address (localhost)
* `0.0.0.0` – Non-routable meta-address (used in routing)
* `169.254.x.x` – Link-local (automatic IP when DHCP fails)
* `255.255.255.255` – Broadcast address

---

## 📁 What is Subnetting?

**Subnetting** is the process of dividing a large IP network into smaller, manageable sub-networks or subnets. It improves network performance and enhances security by containing broadcast traffic and organizing hosts logically.

---

## 🌐 Why Subnet?

* Optimize network performance
* Reduce broadcast domains
* Improve network management and security
* Efficient IP address utilization

---

## 🔢 Subnet Mask

A **subnet mask** determines which portion of the IP address represents the network and which part represents the host.

**Example:**

* IP Address: `192.168.1.10`
* Subnet Mask: `255.255.255.0`
* Network: `192.168.1.0`
* Hosts range: `192.168.1.1 - 192.168.1.254`

---

## 📊 CIDR Notation

CIDR (Classless Inter-Domain Routing) expresses subnets as IP/prefix-length:

**Example:**

* `192.168.1.0/24`

  * `24` bits for network
  * 8 bits for host
  * 2^8 - 2 = 254 usable hosts

---

## 🌎 Subnetting Examples

### Subnetting a /24 Network:

* **Network:** `192.168.1.0/24`
* **Split into two /25 subnets:**

  * `192.168.1.0/25` → 126 hosts
  * `192.168.1.128/25` → 126 hosts

### Subnetting into Four /26 Networks:

* `192.168.1.0/26` → 62 hosts
* `192.168.1.64/26` → 62 hosts
* `192.168.1.128/26` → 62 hosts
* `192.168.1.192/26` → 62 hosts

---

## 🧬 Calculating Subnets

| CIDR | Subnet Mask     | # of Subnets (from /24) | Hosts/Subnet |
| ---- | --------------- | ----------------------- | ------------ |
| /25  | 255.255.255.128 | 2                       | 126          |
| /26  | 255.255.255.192 | 4                       | 62           |
| /27  | 255.255.255.224 | 8                       | 30           |
| /28  | 255.255.255.240 | 16                      | 14           |
| /29  | 255.255.255.248 | 32                      | 6            |
| /30  | 255.255.255.252 | 64                      | 2            |

---

## 💳 Reserved Addresses in a Subnet

Each subnet has two reserved IPs:

* **Network Address:** First IP (identifies the subnet)
* **Broadcast Address:** Last IP (used to reach all hosts in the subnet)

These are not assignable to hosts.

---

## ⚙️ Subnetting Tools

### CLI Commands

```bash
ipcalc 192.168.1.0/25
subnetcalc 192.168.1.0/26
```

### Online Calculators

* subnet-calculator.com
* ipcalc.co

---

## 🌟 Use Cases

* Segmenting users, departments, or servers
* Reducing broadcast traffic
* Network isolation for security
* Designing VPC subnets in cloud platforms

---
