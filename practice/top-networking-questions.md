# Top Networking Interview Questions

### 1. What happens when you type google.com in your browser?
1. Browser checks cache for DNS record. If not found, calls OS.
2. OS queries Resolver (ISP), which queries Root server -> TLD server -> Authoritative Name Server to get the IP.
3. Browser establishes TCP connection (3-way handshake) with server IP on port 443.
4. TLS Handshake takes place for encryption.
5. HTTP GET request is sent.
6. Server handles request and sends back HTTP Response containing HTML.
7. Browser renders HTML.

### 2. Difference between TCP and UDP?
TCP guarantees delivery, maintains order, and handles congestion. Slower.
UDP just blasts packets, no delivery guarantees. Fast. Used in video, VoIP.

### 3. What is a Subnet Mask?
A 32-bit number that masks an IP address and divides the IP address into network address and host address.

### 4. What is a MAC address vs an IP Address?
- MAC is a physical hardware address assigned by the manufacturer. Works at Layer 2.
- IP is a logical address assigned by the network DHCP. Works at Layer 3.

### 5. What are the common ports?
- 21: FTP
- 22: SSH
- 53: DNS
- 80: HTTP
- 443: HTTPS
- 3306: MySQL
