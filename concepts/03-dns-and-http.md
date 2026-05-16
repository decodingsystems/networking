# DNS, HTTP, and HTTPS

## DNS – The Internet's Phonebook

### What is DNS?
The **Domain Name System (DNS)** is the system that translates human-readable domain names (like `google.com`) into machine-readable IP addresses (like `142.250.195.78`). Without DNS, you'd have to memorize IP addresses to visit any website.

### DNS Resolution Process (Step by Step)
1. You type `google.com` in your browser.
2. The OS checks its local **DNS cache** (recently looked-up domains). If found, done!
3. If not cached, it queries the **Recursive Resolver** (usually your ISP's DNS server).
4. The resolver asks a **Root Name Server** → which points to the `.com` **TLD Name Server**.
5. The TLD server points to Google's **Authoritative Name Server**.
6. The Authoritative server returns the IP address.
7. The resolver caches the result and returns it to your browser.

This entire process typically takes < 50ms.

### Common DNS Record Types
- **A Record:** Maps a domain to an IPv4 address.
- **AAAA Record:** Maps a domain to an IPv6 address.
- **CNAME:** Creates an alias from one domain to another.
- **MX Record:** Specifies email servers for the domain.
- **TXT Record:** Stores arbitrary text, widely used for domain verification and SPF/DKIM email security.
- **NS Record:** Lists the Authoritative Name Servers for the domain.

---

## HTTP – The Language of the Web

### What is HTTP?
**Hypertext Transfer Protocol (HTTP)** is the application-layer protocol that governs how web browsers (clients) request content from web servers, and how servers respond. HTTP is **stateless**—each request/response pair is independent; the server retains no memory of previous requests (this is why cookies and sessions exist).

### HTTP Request Anatomy
```
GET /api/users HTTP/1.1
Host: api.example.com
Authorization: Bearer <token>
Content-Type: application/json
```

### HTTP Methods
- `GET`: Retrieve a resource. No body.
- `POST`: Create a new resource. Body contains data.
- `PUT`: Replace a resource entirely.
- `PATCH`: Partially update a resource.
- `DELETE`: Remove a resource.

### HTTP Status Codes
- **200 OK, 201 Created:** Success.
- **301 Moved Permanently, 302 Found:** Redirections.
- **400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found:** Client errors.
- **500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable:** Server errors.

## HTTPS – HTTP Over TLS
**HTTPS** is HTTP secured by **TLS (Transport Layer Security)**. Before HTTP data is exchanged, a **TLS handshake** occurs: the client and server negotiate encryption algorithms and the server presents its certificate (proving its identity), and a shared secret key is derived. All subsequent communication is encrypted.

---

## Hands-on Lab: Querying DNS and Inspecting HTTP Headers

### Objective
Use `dig`, `nslookup`, and `curl` to examine DNS resolution and raw HTTP responses.

### Part 1: DNS Exploration
1. **Basic DNS lookup:**
   ```bash
   dig google.com
   ```
   Look at the **ANSWER SECTION** for the A record IP address.
2. **Check DNS record types:**
   ```bash
   dig google.com MX     # Email servers
   dig google.com TXT    # Verification records
   dig google.com NS     # Authoritative nameservers
   ```
3. **Trace the full DNS resolution chain** (all hops):
   ```bash
   dig +trace google.com
   ```
   You'll see queries to Root → TLD → Authoritative servers live.

### Part 2: HTTP Headers
4. **Fetch HTTP headers only:**
   ```bash
   curl -I http://example.com
   ```
5. **Inspect HTTPS certificate and headers:**
   ```bash
   curl -Iv https://google.com 2>&1 | head -50
   ```
   Look for the `Server`, `Content-Type`, `Strict-Transport-Security` headers and TLS certificate info.
6. **Test HTTP methods with curl:**
   ```bash
   curl -X POST https://jsonplaceholder.typicode.com/posts \
     -H "Content-Type: application/json" \
     -d '{"title": "Test", "body": "Hello World", "userId": 1}'
   ```

### Conclusion
You've traced DNS resolution from your machine to the authoritative server, examined real-world HTTP headers, and made API calls using different HTTP methods.
