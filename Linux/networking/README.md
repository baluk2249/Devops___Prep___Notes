# Essential Linux Network Troubleshooting for DevOps Engineers

## 1. Check Network Connectivity
**Problem:** Unable to reach a remote server.

**Example:**
```bash
ping -c 4 google.com
```
If `ping` fails, it may indicate DNS issues, network disconnection, or firewall restrictions.

---

## 2. Check DNS Resolution
**Problem:** Domain names are not resolving.

**Example:**
```bash
nslookup google.com
dig google.com
```
If these commands fail, check `/etc/resolv.conf` or restart the DNS service.

---

## 3. Check Open Ports on a Server
**Problem:** A service is not accessible.

**Example:**
```bash
netstat -tulnp | grep 80
ss -tulnp | grep 80
```
If the expected service is not listening, restart it or check firewall rules.

---

## 4. Check Firewall Rules
**Problem:** Traffic is being blocked.

**Example:**
```bash
sudo iptables -L -n -v
sudo ufw status
```
Modify firewall rules if necessary.

---

## 5. Check Network Interface Details
**Problem:** Network adapter not working properly.

**Example:**
```bash
ip a
ifconfig -a
```
Ensure the interface is up using:
```bash
sudo ip link set eth0 up
```

---

## 6. Check Route to a Destination
**Problem:** Unable to reach a specific IP.

**Example:**
```bash
traceroute google.com
mtr google.com
```
Identifies network hops and potential routing issues.

---

## 7. Test Connectivity on Specific Port
**Problem:** A service is unreachable on a specific port.

**Example:**
```bash
nc -zv 192.168.1.1 22
telnet 192.168.1.1 22
```
If the connection is refused, the service might not be running or a firewall might be blocking it.

---

## 8. Analyze Network Traffic
**Problem:** Need to debug network traffic issues.

**Example:**
```bash
tcpdump -i eth0 port 80
```
This helps in debugging packet flow issues.

---

## 9. Restart Networking Services
**Problem:** Network issues persist after config changes.

**Example:**
```bash
sudo systemctl restart networking
sudo systemctl restart NetworkManager
```

---

## 10. Check External IP Address
**Problem:** Need to confirm public IP.

**Example:**
```bash
curl -s ifconfig.me
```
This helps verify NAT and external connectivity.
