# Networking Commands Cheatsheet

## Windows
- `ipconfig`: Show IP configuration.
- `ipconfig /flushdns`: Clear DNS cache.
- `ping <target>`: Check packet route to host.
- `tracert <target>`: Trace route to a remote host.
- `nslookup <domain>`: Query DNS records.
- `netstat -ano`: Display active network connections and ports.

## Linux / macOS
- `ifconfig` or `ip a`: Show IP configuration.
- `ping -c 4 <target>`: Send 4 ping requests.
- `traceroute <target>`: Trace route to a host.
- `dig <domain>`: Advanced DNS lookup.
- `curl -I <url>`: Fetch HTTP headers.
- `netstat -tulpen` or `ss -tulpen`: Show listening sockets and their PIDs.
