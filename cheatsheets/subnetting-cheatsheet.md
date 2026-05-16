# Subnetting Cheatsheet

## IPv4 Classes
- **Class A:** `1.0.0.0` to `126.255.255.255` (Subnet: `255.0.0.0` or `/8`)
- **Class B:** `128.0.0.0` to `191.255.255.255` (Subnet: `255.255.0.0` or `/16`)
- **Class C:** `192.0.0.0` to `223.255.255.255` (Subnet: `255.255.255.0` or `/24`)

## CIDR Notation Quick Ref
- `/24`: 256 IPs (254 usable)
- `/25`: 128 IPs (126 usable)
- `/26`: 64 IPs (62 usable)
- `/27`: 32 IPs (30 usable)
- `/28`: 16 IPs (14 usable)
- `/29`: 8 IPs (6 usable)
- `/30`: 4 IPs (2 usable - usually point-to-point links)

## Private IP Ranges (RFC 1918)
- `10.0.0.0 - 10.255.255.255`
- `172.16.0.0 - 172.31.255.255`
- `192.168.0.0 - 192.168.255.255`
