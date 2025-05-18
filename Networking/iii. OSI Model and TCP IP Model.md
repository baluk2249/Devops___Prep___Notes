## OSI Model (Open Systems Interconnection)

The OSI model is a conceptual framework used to understand and standardize the functions of a telecommunication or computing system without regard to its underlying internal structure and technology.

---

## 🧱 7 Layers of the OSI Model

| Layer | Name         | Function                                          | Example Protocols                      |
| ----- | ------------ | ------------------------------------------------- | -------------------------------------- |
| 7     | Application  | User interface, end-user services                 | HTTP, FTP, SMTP                        |
| 6     | Presentation | Data translation, encryption, compression         | SSL/TLS, JPEG, GIF, ASCII              |
| 5     | Session      | Establishes, manages, and terminates connections  | NetBIOS, RPC                           |
| 4     | Transport    | Reliable data transfer, error recovery            | TCP, UDP                               |
| 3     | Network      | Path determination, logical addressing            | IP, ICMP, IGMP                         |
| 2     | Data Link    | Physical addressing, error detection              | Ethernet, PPP, Switches                |
| 1     | Physical     | Transmits raw bit stream over the physical medium | Cables, Hubs, NICs, Electrical signals |

---

## 🔍 Detailed Layer Functions

### Layer 7: Application

* Closest to the user
* Provides services like email, file transfer, and web browsing
* **Example:** A user accessing a website using HTTP

### Layer 6: Presentation

* Translates data between the application and the network format
* Handles encryption and data compression
* **Example:** TLS encrypting HTTP into HTTPS

### Layer 5: Session

* Manages and controls dialog between two devices
* Establishes, maintains, and terminates sessions
* **Example:** Remote Procedure Call (RPC) services

### Layer 4: Transport

* Ensures complete data transfer with reliability and flow control
* **TCP:** Connection-oriented
* **UDP:** Connectionless
* **Example:** TCP breaking large files into segments

### Layer 3: Network

* Responsible for logical addressing and routing
* Determines best path to route the data
* **Example:** IP packet routing through routers

### Layer 2: Data Link

* Responsible for physical addressing (MAC) and error detection
* Divided into MAC and LLC sublayers
* **Example:** Ethernet addressing via MAC addresses

### Layer 1: Physical

* Concerned with the transmission of raw bits
* Defines hardware elements: cables, cards, voltages
* **Example:** Sending electrical signals through a network cable

---

## 🎓 OSI Model Example Scenario

**Sending an Email:**

1. **Application:** User composes email via an email client (SMTP)
2. **Presentation:** Email is converted into ASCII format
3. **Session:** Session is established between sender and server
4. **Transport:** TCP segments the message and ensures delivery
5. **Network:** IP adds destination address and routes the data
6. **Data Link:** MAC address added and data framed
7. **Physical:** Data transmitted as bits over Ethernet cable

---



## 📂 TCP/IP Model Overview

The TCP/IP model (also known as the Internet Protocol Suite) is a more practical and widely used model compared to OSI. It consists of 4 layers:

| Layer          | Corresponds to OSI Layers                      | Function                              | Protocols          |
| -------------- | ---------------------------------------------- | ------------------------------------- | ------------------ |
| Application    | 7 - Application, 6 - Presentation, 5 - Session | End-user services and network process | HTTP, FTP, SMTP    |
| Transport      | 4 - Transport                                  | Reliable/Unreliable delivery          | TCP, UDP           |
| Internet       | 3 - Network                                    | Logical addressing, routing           | IP, ICMP           |
| Network Access | 2 - Data Link, 1 - Physical                    | Physical transmission of data         | Ethernet, ARP, MAC |

### Comparison with OSI:

* OSI has 7 layers, TCP/IP has 4.
* OSI is theoretical; TCP/IP is implementation-focused.
* TCP/IP layers combine some OSI layers:

  * Application = OSI Layers 5-7
  * Network Access = OSI Layers 1-2

### Example Data Flow (Web Request):

1. **Application Layer:** User enters URL, HTTP request is generated
2. **Transport Layer:** TCP segments the HTTP request
3. **Internet Layer:** IP adds destination address
4. **Network Access Layer:** Data is sent over physical medium

TCP/IP provides a more streamlined and practical approach used in real-world networking.

