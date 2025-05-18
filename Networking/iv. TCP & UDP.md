# TCP and UDP

## Introduction

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are core protocols of the Internet Protocol Suite. They both reside in the transport layer of the OSI and TCP/IP models and are used for transmitting data between devices over a network.

---

## TCP (Transmission Control Protocol)

### Characteristics:

* **Connection-oriented** protocol.
* Reliable and ensures data is delivered in the same order it was sent.
* Performs error-checking and recovery.
* Supports congestion control and flow control.
* Slower than UDP due to additional overhead.

### Key Features:

1. **Three-way Handshake** (SYN, SYN-ACK, ACK):

   * Initiates a connection between client and server.

2. **Reliable Data Transfer**:

   * Ensures data is received and acknowledged.

3. **Ordered Delivery**:

   * Segments are reassembled in the correct order.

4. **Error Detection and Correction**:

   * Uses checksums and retransmits lost packets.

5. **Flow Control**:

   * Prevents sender from overwhelming the receiver (using window size).

6. **Congestion Control**:

   * Adjusts transmission rate to avoid congestion.

### Use Cases:

* Web browsing (HTTP, HTTPS)
* Email (SMTP, IMAP, POP3)
* File transfer (FTP, SFTP)

### Example (TCP 3-way handshake):

```text
Client          Server
  | SYN --------> |
  | <---- SYN-ACK |
  | ACK --------> |
Connection Established
```

---

## UDP (User Datagram Protocol)

### Characteristics:

* **Connectionless** protocol.
* Unreliable and does not guarantee delivery, order, or duplicate protection.
* Low overhead and faster than TCP.
* No congestion or flow control.

### Key Features:

1. **No Connection Establishment**:

   * No handshaking, can send data immediately.

2. **Unreliable Transmission**:

   * Packets may be lost or arrive out of order.

3. **No Overhead for Reliability**:

   * No acknowledgment or retransmission.

4. **Faster and Lightweight**:

   * Suitable for time-sensitive applications.

### Use Cases:

* Streaming (audio/video)
* Online gaming
* DNS queries
* VoIP (Voice over IP)

### Example:

```text
Client          Server
  | Data Packet --> |
(No handshake, no acknowledgment)
```

---

## Comparison Table:

| Feature              | TCP                   | UDP                  |
| -------------------- | --------------------- | -------------------- |
| Connection           | Connection-oriented   | Connectionless       |
| Reliability          | Reliable              | Unreliable           |
| Order of Delivery    | Guaranteed            | Not guaranteed       |
| Error Checking       | Yes (with correction) | Yes (no correction)  |
| Acknowledgments      | Yes                   | No                   |
| Flow/Congestion Ctrl | Yes                   | No                   |
| Speed                | Slower                | Faster               |
| Overhead             | High                  | Low                  |
| Use Case Example     | HTTP, FTP, Email      | DNS, Streaming, VoIP |

---

## Summary:

* **TCP** is best for applications requiring reliability, ordered delivery, and data integrity.
* **UDP** is suited for real-time, low-latency applications where speed is critical and occasional data loss is acceptable.

