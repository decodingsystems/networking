# The OSI Model — 7 Layers of Network Communication

## What is the OSI Model?
The **OSI (Open Systems Interconnection)** model is a conceptual framework that standardizes how different computer systems communicate over a network. Developed by ISO in 1984, it divides network communication into **7 distinct layers**, each with specific responsibilities.

The OSI model is not how modern networks literally work (TCP/IP is the real-world implementation), but it's the universal language used to describe, debug, and reason about network behavior.

## The 7 Layers

| Layer | Name | Key Protocols/Technologies | PDU |
|-------|------|---------------------------|-----|
| 7 | **Application** | HTTP, FTP, SMTP, DNS, SSH | Data |
| 6 | **Presentation** | SSL/TLS, JPEG, MPEG, ASCII | Data |
| 5 | **Session** | NetBIOS, RPC, PPTP | Data |
| 4 | **Transport** | TCP, UDP | Segment |
| 3 | **Network** | IP, ICMP, OSPF, BGP | Packet |
| 2 | **Data Link** | Ethernet, MAC, Wi-Fi (802.11) | Frame |
| 1 | **Physical** | Cables, fiber, radio waves | Bits |

**PDU (Protocol Data Unit):** The name for the data unit at each layer.

## Layer-by-Layer Breakdown

### Layer 7 — Application
The only layer that directly interacts with the user. Provides protocols that applications use to send and receive data. **What it does:** Provides the interface for user-facing services.

### Layer 6 — Presentation
Translates data formats, handles encryption/decryption (SSL/TLS ends here), and compression. **Think:** Translator between application and network formats.

### Layer 5 — Session
Establishes, manages, and terminates connections (sessions) between applications. Handles authentication and reconnection. **Think:** The meeting manager.

### Layer 4 — Transport
Provides **end-to-end** communication between processes on different hosts:
- **TCP:** Reliable, ordered, error-checked delivery. 3-way handshake. Used by HTTP, FTP, SMTP.
- **UDP:** Unreliable, no connection, fast. Used by DNS, video streaming, gaming.

### Layer 3 — Network
Responsible for logical addressing (**IP addresses**) and routing packets across multiple networks. Routers operate at this layer. Key protocols: IP, ICMP (`ping`), routing protocols (OSPF, BGP).

### Layer 2 — Data Link
Frames data for transmission over a physical link and handles **MAC addressing**. Switches operate at this layer. Error detection (but not correction) via CRC.

### Layer 1 — Physical
The actual physical transmission: voltages on copper, light pulses on fiber, radio waves for Wi-Fi. No addressing — just raw bits.

## Encapsulation — How Data Travels Down the Stack
When you send an HTTP request:
```
Application:    HTTP data
Transport:      + TCP Header (src/dst port, seq number)   → Segment
Network:        + IP Header (src/dst IP)                  → Packet
Data Link:      + Ethernet Header (src/dst MAC) + Trailer → Frame
Physical:       101010101... (bits on wire)
```
Each layer wraps the data from the layer above with its own header (**encapsulation**). The receiver unwraps in reverse (**de-encapsulation**).

## Mnemonics
- **Top-down (7→1):** "**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing"
- **Bottom-up (1→7):** "**P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way"
