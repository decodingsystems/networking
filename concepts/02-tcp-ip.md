# TCP/IP Model & Core Protocols

## Background
While the OSI model is a conceptual framework for understanding networking, the real Internet runs on the **TCP/IP model** (also called the Internet Protocol Suite). Developed in the 1970s by DARPA, it was designed to be robust, decentralized, and fault-tolerant—so that communication could survive partial network failures during a nuclear attack.

The TCP/IP stack is more practical and less granular than OSI, compressing 7 layers into 4.

## The 4 Layers

### Layer 1 – Network Access Layer (Link Layer)
Covers what OSI calls Physical and Data Link. Responsible for how data is placed on the physical network medium. This includes Ethernet and Wi-Fi protocols, MAC addressing, and ARP (Address Resolution Protocol), which maps IP addresses to MAC addresses.

### Layer 2 – Internet Layer
Corresponds to OSI's Network layer. The Internet Protocol (IP) operates here, responsible for **logical addressing** (IP addresses) and **routing** packets across different networks. Two versions: IPv4 (32-bit, ~4.3 billion addresses) and IPv6 (128-bit, virtually unlimited addresses). ICMP (used by `ping`) also operates at this layer.

### Layer 3 – Transport Layer
The critical layer for application communication. Two primary protocols:

**TCP (Transmission Control Protocol)** – Connection-oriented. Before data can flow, a **3-Way Handshake** must occur:
1. Client sends **SYN** (synchronize).
2. Server replies with **SYN-ACK**.
3. Client sends **ACK**.

TCP guarantees delivery through acknowledgments (ACKs). Missing packets are retransmitted. Packets are reordered if they arrive out of sequence. Flow control prevents a fast sender from overwhelming a slow receiver. Use cases: Web browsing (HTTP/S), email (SMTP), file transfer (FTP).

**UDP (User Datagram Protocol)** – Connectionless. No handshake, no delivery guarantees, no ordering. Just fire packets and hope they arrive. Extremely fast and low overhead. Use cases: Streaming video (HLS), online gaming, DNS queries, VoIP.

### Layer 4 – Application Layer
Where user-facing protocols live: HTTP (web), HTTPS (encrypted web), DNS (name resolution), FTP (file transfer), SSH (remote access), SMTP (email), and many more.

## Ports
Ports allow a single machine to run many network services simultaneously. Ports 0–1023 are "well-known ports" reserved for standard services (Port 80 = HTTP, Port 443 = HTTPS, Port 22 = SSH, Port 53 = DNS).

---

## Hands-on Lab: Observing TCP 3-Way Handshake

### Objective
Capture and observe the TCP 3-way handshake in Wireshark to understand how TCP connections are established.

### Steps
1. **Open Wireshark** and select your active network interface.
2. **Start capture**, then in your terminal run:
   ```bash
   curl http://example.com
   ```
3. **Stop capture** in Wireshark.
4. **Filter** by typing `tcp && http` in the filter bar and pressing Enter.
5. **Locate the SYN packet:** Look for a packet going to port 80 with flags `[SYN]`.
6. **Trace the handshake:** Right-click that SYN packet → Follow → TCP Stream.
   - You'll see: `SYN` → `SYN-ACK` → `ACK` completing the connection.
   - Then the HTTP GET request and response.
7. **Observe the teardown:** After the response, look for `FIN-ACK` packets ending the connection.

### Bonus: Compare with UDP
Run a DNS lookup and observe UDP:
```bash
dig google.com
```
In Wireshark filter: `udp && dns`. You'll see a **single request/response** with no handshake—direct and fast.

### Conclusion
You've visually observed the TCP 3-way handshake and the absence of any connection setup overhead in UDP, making the trade-off between reliability and speed tangible.
