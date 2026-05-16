# Lab: Basic Packet Analysis

## Objective
Learn how to use packet sniffing tools to observe network traffic in real-time.

## Prerequisites
- Download and install **Wireshark**.
- Administrator / Root permissions.

## Exercise: Capturing Traffic
1. Open Wireshark.
2. Select your active network interface (e.g., `Wi-Fi` or `eth0`).
3. Click the "Start" button (Shark fin icon) to begin capturing packets.
4. Open a web browser and go to `http://example.com` (Note: not HTTPS).
5. Stop the capture by clicking the red square stop button in Wireshark.

## Exercise: Filtering Traffic
1. In the Wireshark filter bar, type `http` and press Enter.
2. Find the packet with `Info` starting with `GET / HTTP/1.1`.
3. Select the packet and look at the detailed pane below.
   - Expand **Ethernet II**: You can see source and destination MAC.
   - Expand **Internet Protocol Version 4**: Locate Source IP and Dest IP.
   - Expand **Transmission Control Protocol**: See the Source Port and Dest Port (80).
   - Expand **Hypertext Transfer Protocol**: See the raw GET request string.

## Conclusion
You have successfully intercepted, filtered, and analyzed a raw HTTP packet using Wireshark.
