# Active Reconnaissance – Room Summary

## Overview
This room introduced the fundamentals of **Active Reconnaissance**, where a tester directly interacts with a target system to gather information. Unlike passive recon, this approach generates traffic that can be logged, monitored, and potentially detected by security systems such as firewalls, IDS/IPS, and WAFs.

The room covered five core tools: **web browser (DevTools), ping, traceroute, telnet, and netcat**, demonstrating how each contributes to building a clearer picture of a target system before advanced scanning.

---

## Key Findings

### 1. Web Browser & Developer Tools
- Revealed hidden information such as:
  - Server headers
  - JavaScript source files
  - Cookies and local storage data
  - SSL certificate details (including SANs)
- Helped identify technologies used on the target website.

### 2. Ping (ICMP)
- Verified host availability and network reachability.
- TTL values provided indirect OS fingerprinting hints (Linux vs Windows).
- Showed whether ICMP traffic is allowed or filtered.

### 3. Traceroute
- Mapped the full network path between attacker and target.
- Identified intermediate routers (hops).
- Showed that routing paths are dynamic and may change between runs.

### 4. Telnet
- Demonstrated banner grabbing on TCP services (e.g., HTTP port 80).
- Revealed server software and version information (e.g., Apache 2.4.61).
- Highlighted insecure nature of plaintext protocols.

### 5. Netcat (nc)
- Used for banner grabbing similar to telnet but more flexible.
- Connected to services like FTP to extract version information.
- Showed ability to act as both client and simple listener for TCP communication.

---

## Security Impact

- **Information Disclosure:** Service banners and headers expose software versions that attackers can use to identify known vulnerabilities (CVE-based exploitation).
- **Network Mapping Risk:** Traceroute reveals internal routing infrastructure, which can assist attackers in understanding network topology.
- **Host Discovery Exposure:** Ping responses confirm live systems and may leak OS hints via TTL analysis.
- **Legacy Protocol Risks:** Telnet exposes credentials and data in plaintext if used in real environments.
- **Reconnaissance Detection:** All active recon techniques generate logs that can be detected by firewalls, IDS/IPS, and SIEM systems, enabling defenders to identify scanning activity early.

---

## Remediation Recommendations

- **Minimize Information Exposure**
  - Disable or modify server banners (e.g., hide Apache/Nginx version headers).
  - Remove unnecessary JavaScript comments and hardcoded endpoints.

- **Network Hardening**
  - Block or rate-limit ICMP (ping) where not required.
  - Restrict or filter traceroute responses where appropriate.

- **Replace Insecure Protocols**
  - Disable Telnet entirely and use **SSH** for remote administration.
  - Avoid plaintext services for authentication and management.

- **Security Monitoring**
  - Implement IDS/IPS rules to detect scanning patterns (ping sweeps, port probing).
  - Monitor logs for unusual DevTools-like browsing patterns and repeated connection attempts.

- **Secure Service Configuration**
  - Use HTTPS with proper TLS configuration.
  - Limit exposed service versions and apply regular patching.

---

## Conclusion
This room demonstrates how simple tools can be combined to perform effective **early-stage reconnaissance**. While each tool individually provides limited information, together they form a powerful workflow for mapping, identifying, and understanding a target system before deeper penetration testing begins.
