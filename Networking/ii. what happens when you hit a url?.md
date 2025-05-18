# What Happens When You Hit a URL in a Web Browser

---

## 1. Entering URL and DNS Resolution 🌐

When you enter a URL (e.g., `https://www.example.com`) in your browser:

### Step 1: Browser Cache Lookup
- The browser checks if it already has the IP address cached.

### Step 2: OS Cache and Hosts File
- If not found, it checks the OS cache and the hosts file.

### Step 3: Query DNS Resolver
- If still unresolved, the browser sends a DNS query to the configured DNS server (e.g., ISP DNS or Google DNS `8.8.8.8`).

### Step 4: Recursive DNS Lookup
- The DNS resolver queries root DNS servers → TLD DNS servers (like `.com`) → Authoritative DNS servers for the domain.

### Step 5: Receive IP Address
- The authoritative DNS server returns the IP address (e.g., `93.184.216.34`).

**Example:**

```bash
nslookup www.example.com
```

---

## 2. TCP Handshake 🤝

After obtaining the IP, the browser establishes a TCP connection (usually port 80 for HTTP or 443 for HTTPS).

### The 3-Way Handshake:

| Step  | Description                                    |
|--------|------------------------------------------------|
| SYN    | Client sends a SYN packet to initiate connection. |
| SYN-ACK| Server responds with SYN-ACK to acknowledge.    |
| ACK    | Client sends ACK to confirm the connection.      |

This ensures a reliable connection is established.

**Example:**

```bash
telnet www.example.com 80
```

---

## 3. TLS Handshake 🔒 (For HTTPS)

If the URL uses HTTPS, a TLS handshake happens after the TCP connection:

### TLS Handshake Steps:

1. **Client Hello:** Client sends supported TLS versions, cipher suites, and a random nonce.
2. **Server Hello:** Server selects TLS version, cipher suite, and sends its certificate.
3. **Certificate Verification:** Client verifies server’s certificate via trusted Certificate Authority (CA).
4. **Key Exchange:** Secure keys are exchanged (e.g., using Diffie-Hellman).
5. **Finished:** Both sides confirm handshake completion and begin encrypted communication.

**Example:**

```bash
openssl s_client -connect www.example.com:443
```

---

## 4. HTTP Request & Response 🌍

Once the connection is established:

- Browser sends an HTTP request (e.g., GET `/index.html`).
- Server processes the request and sends back a response (HTML, JSON, images).
- Browser renders the response content.

**Example HTTP GET request:**

```
GET /index.html HTTP/1.1
Host: www.example.com
```

---

## Summary Flow

1. DNS Resolution (URL → IP)
2. TCP Handshake (establish connection)
3. TLS Handshake (secure connection for HTTPS)
4. HTTP Request/Response

---

## Additional Notes

- Caching at browser and DNS resolver speeds up repeated lookups.
- HTTP/2 and HTTP/3 optimize connections further with multiplexing.
- TLS versions and cipher suites affect connection security.
- Persistent TCP connections reduce overhead on subsequent requests.

---
