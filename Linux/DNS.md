#  DNS 

## What is DNS?

**DNS (Domain Name System)** is a hierarchical and decentralized naming system used to translate human-readable domain names (like `example.com`) into IP addresses (like `93.184.216.34`) that computers use to identify each other on the network.

---

## How DNS Works

When you type a website URL into your browser, the following steps occur:

1. **Browser Cache Check** – The browser checks its cache for a recently resolved IP.
2. **OS Cache Check** – The OS checks its local DNS cache.
3. **DNS Resolver Query** – If not cached, the request goes to a configured DNS resolver.
4. **Recursive Query** – The resolver queries:

   * Root DNS servers (.)
   * TLD DNS servers (e.g., `.com`, `.org`)
   * Authoritative DNS server for the domain
5. **IP Address Returned** – The resolved IP is returned to the client.
6. **Website Access** – Browser connects to the IP address.

---

## Key DNS Components

| Component            | Description                                      |
| -------------------- | ------------------------------------------------ |
| Resolver             | Client-side DNS component that initiates queries |
| Root Server          | Top-level DNS server, knows about TLDs           |
| TLD Server           | Handles Top-Level Domains like `.com`, `.org`    |
| Authoritative Server | Provides actual IP address for the domain        |
| Records              | DNS data stored (A, AAAA, MX, CNAME, etc.)       |

---

## Detailed Notes on Key DNS Servers

### Root DNS Servers

* The **root servers** are the first step in translating human-readable domain names into IP addresses.
* There are 13 logical root servers, named A to M, operated by various organizations worldwide (e.g., Verisign, ICANN).
* Each root server is actually a cluster of many servers distributed globally using Anycast.
* They don’t know the actual IP address of domains but direct queries to the appropriate TLD name servers.

**Example:**

```bash
dig . NS
```

This command lists the root name servers.

### TLD DNS Servers

* **Top-Level Domain (TLD) servers** store information about authoritative name servers for domains within a specific TLD like `.com`, `.net`, `.org`, `.edu`, etc.
* TLDs are managed by registries like Verisign (for `.com`) or PIR (for `.org`).

**Example:**

```bash
dig com. NS
```

Returns the nameservers for the `.com` TLD.

### Authoritative DNS Servers

* These are the DNS servers that have the final answer for a domain.
* They contain the zone file for a domain including all resource records.
* Managed by the domain’s hosting provider or a third-party DNS service.

**Example:**

```bash
dig example.com @ns1.exampledns.com
```

Queries the authoritative name server `ns1.exampledns.com` directly for `example.com`.

---

## Common DNS Record Types

| Record Type | Description                                            |
| ----------- | ------------------------------------------------------ |
| `A`         | IPv4 address of a domain                               |
| `AAAA`      | IPv6 address of a domain                               |
| `CNAME`     | Canonical name (alias to another domain)               |
| `MX`        | Mail exchange (used for email routing)                 |
| `NS`        | Nameserver for the domain                              |
| `TXT`       | Text records for verification and policies (e.g., SPF) |
| `PTR`       | Pointer record (used for reverse DNS lookup)           |

---

## Useful DNS Tools with Examples

### 1. `nslookup`

```bash
nslookup example.com
```

### 2. `dig`

```bash
dig example.com
```

```bash
dig +short example.com A
```

### 3. `host`

```bash
host example.com
```

### 4. Reverse Lookup

```bash
nslookup 93.184.216.34
```

```bash
dig -x 93.184.216.34
```

### 5. View NS Records

```bash
dig example.com NS
```

### 6. Query Specific DNS Server

```bash
dig @8.8.8.8 example.com
```

---

## Real-World Use Cases

* **Website Troubleshooting**: Check DNS resolution issues.
* **Email Configuration**: Verify MX and SPF records.
* **Security**: Monitor for spoofed or incorrect records.
* **Network Diagnostics**: Perform reverse lookups.
* **Load Balancing**: Use multiple A records or geo-DNS.

---

## DNS Caching

* **Positive Caching**: Stores successful lookups.
* **Negative Caching**: Stores failed lookups.
* **TTL (Time to Live)**: How long DNS data is cached.

Flush DNS cache examples:

* Windows:

  ```bash
  ipconfig /flushdns
  ```
* macOS:

  ```bash
  sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
  ```
* Linux:

  ```bash
  sudo systemd-resolve --flush-caches
  ```

---

