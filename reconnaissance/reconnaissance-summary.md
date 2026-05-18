
🛰️ TryHackMe Room Report: Active Reconnaissance
🧾 Executive Summary

This room focused on the fundamentals of Active Reconnaissance, a process where a tester directly communicates with target systems to gather useful information. Unlike passive reconnaissance, active recon generates observable network traffic that can be detected and logged by defensive security solutions.

The exercise demonstrated how basic networking and enumeration tools can be used to identify hosts, map network paths, collect service information, and reveal technologies running on target systems.

The room primarily explored the use of:

Web Browser Developer Tools
Ping
Traceroute
Telnet
Netcat (nc)

Together, these tools provide valuable intelligence that can support later phases of penetration testing and vulnerability assessment.

🔍 Assessment Findings
🌐 1. Web Browser & Developer Tools Enumeration

Using browser-based developer tools, multiple forms of hidden and publicly accessible information were identified from the target website.

Information Gathered:
HTTP response headers
Server software details
JavaScript source files
Cookies and local storage data
SSL/TLS certificate information
Subject Alternative Names (SANs)
Security Observation:

The collected information helped identify the technologies and frameworks used by the target application, which could assist attackers in selecting targeted exploits.

📡 2. Host Discovery Using Ping (ICMP)

ICMP echo requests were used to determine whether the target system was online and reachable.

Findings:
Successful responses confirmed active hosts
Round-trip time indicated network latency
TTL values provided indirect operating system fingerprinting hints
Example:
Lower TTL values commonly suggested Linux-based systems
Higher TTL values suggested Windows environments
🌍 3. Network Path Enumeration with Traceroute

Traceroute was used to identify the routing path between the attacker and target system.

Information Identified:
Intermediate routers (network hops)
Approximate geographical routing path
Network latency between hops
Observation:

The routing path changed during repeated tests, demonstrating dynamic routing behavior across networks.

🔌 4. Banner Grabbing with Telnet

Telnet was used to manually connect to open TCP ports and retrieve service banners.

Example Information Retrieved:
Web server type
Software version details
HTTP response headers
Security Concern:

Service banners exposed detailed version information that may help attackers identify known vulnerabilities associated with outdated software.

🛠️ 5. Service Enumeration Using Netcat (nc)

Netcat was utilized for flexible TCP communication and banner grabbing.

Capabilities Demonstrated:
Connecting to open ports
Retrieving FTP/HTTP service banners
Testing TCP communication manually
Acting as a simple listener for incoming connections
Observation:

Netcat provided more flexibility compared to telnet and is commonly used during reconnaissance and exploitation phases.

⚠️ Security Impact Analysis
🔓 Information Disclosure Risk

Server banners, headers, and certificates exposed technology stack details and software versions that could be mapped to publicly known vulnerabilities (CVEs).

🌐 Network Topology Exposure

Traceroute revealed portions of the network infrastructure and routing paths, potentially assisting attackers in network mapping activities.

📡 Host Discovery Exposure

ICMP responses confirmed which systems were active on the network and leaked OS fingerprinting hints through TTL analysis.

⚠️ Insecure Protocol Usage

Telnet communications occur in plaintext, making credentials and transmitted data vulnerable to interception.

🚨 Reconnaissance Detection

All active reconnaissance activities generated detectable network traffic that could be logged by:

Firewalls
IDS/IPS solutions
SIEM platforms
Web Application Firewalls (WAFs)

This creates opportunities for defenders to detect malicious scanning behavior early.

🛡️ Remediation Recommendations
🔧 1. Reduce Information Exposure

Organizations should:

Disable detailed server banners
Remove unnecessary headers
Avoid exposing software versions publicly
Minimize sensitive information inside JavaScript files
🚫 2. Harden Network Services

Implement controls such as:

Blocking unnecessary ICMP traffic
Rate-limiting ping requests
Restricting traceroute visibility where appropriate
🔐 3. Replace Legacy Protocols

Telnet should be fully disabled and replaced with secure alternatives such as:

SSH
Secure management protocols

Plaintext authentication methods should never be used in production environments.

🔥 4. Improve Monitoring & Detection

Security teams should:

Monitor scanning behavior
Detect repeated connection attempts
Create IDS/IPS signatures for reconnaissance activities
Analyze logs for suspicious enumeration patterns
📊 5. Secure Service Configuration

Ensure:

HTTPS is properly configured
TLS versions are secure
Services are regularly patched
Unused ports and services are disabled
📌 Final Conclusion

This room demonstrated how basic active reconnaissance techniques can provide valuable intelligence about a target system and network environment.

Although each tool reveals limited information individually, combining their outputs enables attackers to:

Identify live systems
Discover running services
Map network paths
Fingerprint operating systems
Detect potential attack surfaces

The exercise highlights the importance of secure service configuration, minimizing exposed information, replacing insecure legacy protocols, and continuously monitoring reconnaissance-related activities across enterprise environments.
