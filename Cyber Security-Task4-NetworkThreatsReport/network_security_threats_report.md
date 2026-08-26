# Research Report: Common Network Security Threats

## 1. Introduction
Network security threats matter significantly in today's landscape because enterprise architectures rely heavily on interconnected systems and protocols, making any vulnerability a potential entry point for attackers. A successful breach can lead to severe consequences, including data theft, operational disruption, financial losses, and reputational damage[cite: 3]. With 90% of organizations reporting they were victims of DNS-related attacks in 2023 alone[cite: 3], understanding and mitigating these threats is critical for protecting infrastructure and maintaining business continuity.

## 2. Denial of Service (DoS) and Distributed Denial of Service (DDoS) Attacks
*   **Mechanism:** A DoS attack attempts to deplete a target system's resources, causing it to become unavailable or crash. This can involve flooding the target with UDP, TCP, or ICMP echo (ping) packets until the server cannot accept new connections. In a DDoS attack, the attacker uses a master controller to command infected devices (bots) to launch a coordinated flood.
*   **Real-World Example:** The 2016 Dyn cyberattack used the Mirai botnet (a massive network of compromised loT devices) to launch a DDoS attack, taking down major sites like Twitter, Reddit, and Netflix.
*   **Impact:** Complete loss of service availability, leading to lost revenue and severe operational disruption.
*   **Mitigation Strategies:**
    1.  Deploy rate limiting and IP filtering to drop malformed or excessive packets at the network edge.
    2.  Implement a Web Application Firewall (WAF) and cloud-based DDoS protection services (like Cloudflare or AWS Shield) to absorb traffic spikes.
    3.  Use IP Source Guard and DHCP snooping on network switches.

## 3. Man-in-the-Middle (MitM) Attacks
*   **Mechanism:** An attacker positions themselves in the middle of the communication path between two devices. This allows them to silently eavesdrop on the communication, intercept credentials, or even modify the data being sent between the parties. One common example on local networks is ARP poisoning.
*   **Real-World Example:** The 2015 Superfish scandal involved Lenovo pre-installing adware that intercepted encrypted web traffic by installing its own self-signed root certificate, effectively executing a localized MitM attack.
*   **Impact:** Compromise of sensitive data in transit, including passwords, financial details, and proprietary communications.
*   **Mitigation Strategies:**
    1.  Enforce HTTPS and use HTTP Strict Transport Security (HSTS) for all web traffic to encrypt data in transit.
    2.  Implement Dynamic ARP Inspection (DAI) to prevent ARP poisoning on local networks.
    3.  Avoid using unauthenticated and unencrypted communication channels to transmit sensitive data.

## 4. IP Spoofing
*   **Mechanism:** IP address spoofing involves creating Internet Protocol (IP) packets with a forged source IP address. Attackers use this to conceal their identity, impersonate a trusted machine, or bypass IP-based authentication controls.
*   **Real-World Example:** In the 2018 GitHub DDoS attack, attackers spoofed the IP address of GitHub to send requests to Memcached servers, which then reflected massively amplified responses back to GitHub.
*   **Impact:** Enables amplification attacks, bypasses firewall rules based on IP whitelists, and complicates incident response by hiding the attacker's true origin.
*   **Mitigation Strategies:**
    1.  Implement strict ingress and egress filtering on network edge routers to drop packets with spoofed source addresses.
    2.  Use cryptographic authentication protocols (like IPsec) that do not rely solely on IP addresses for identity verification.
    3.  Deploy Deep Packet Inspection (DPI) firewalls to analyze packet headers and detect anomalies.

## 5. DNS Poisoning/Spoofing
*   **Mechanism:** DNS poisoning targets DNS resolvers by injecting fake data into the cache, redirecting users to malicious websites instead of their intended destinations[cite: 1]. Since the resolver caches the false record, anyone relying on it will be misdirected until the cache clears[cite: 3].
*   **Real-World Example:** In a 2018 attack on MyEtherWallet, attackers used DNS poisoning to trick users into entering their credentials on a fake site, resulting in the theft of over $17 million in Ethereum[cite: 1].
*   **Impact:** Widespread credential theft, distribution of malware, and interception of sensitive communications[cite: 1]. 
*   **Mitigation Strategies:**
    1.  Enable DNSSEC (DNS Security Extensions) to digitally sign DNS records, ensuring data integrity and preventing tampering[cite: 1].
    2.  Use encrypted DNS protocols such as DNS over HTTPS (DoH) or DNS over TLS (DoT)[cite: 1].
    3.  Regularly patch DNS servers and ensure correct configuration of time-to-live (TTL) values for cached data[cite: 1].

## 6. Attack Comparison

| Attack Type | Attack Vector | Who is at Risk | Difficulty to Execute | Ease of Mitigation |
| :--- | :--- | :--- | :--- | :--- |
| **DoS/DDoS** | Botnets, Packet Flooding | Any internet-facing service | Low (via DDoS-for-hire) | Medium (requires specialized mitigation services) |
| **MitM** | ARP Poisoning, Rogue Wi-Fi | End-users on unsecured networks | Medium | Easy (enforcing strong encryption) |
| **IP Spoofing** | Forged Packet Headers | Trust-based networks | Medium | Easy (network edge filtering) |
| **DNS Poisoning** | Malicious Cache Injection | Organizations managing DNS resolvers | High | Medium (DNSSEC implementation can be complex) |

## 7. Conclusion: Key Takeaways for Network Administrators
1.  **Defense in Depth is Essential:** No single control can stop all attacks. Network administrators must deploy a layered security approach combining firewalls, traffic encryption, and secure DNS protocols[cite: 3].
2.  **Verify, Do Not Trust:** Relying on simple identifiers like IP addresses for access control is fundamentally flawed due to spoofing. Implement zero trust architectures and robust authentication protocols.
3.  **Proactive Monitoring:** Since threats like DNS poisoning and MitM attacks often operate silently, continuous monitoring of DNS activity[cite: 3] and network anomalies is required to detect an attack before severe damage occurs.

## 8. References
1. CISA (Cybersecurity and Infrastructure Security Agency). *Understanding Denial-of-Service Attacks*. 
2. Huntress. *What Is DNS Poisoning? Attacks & Prevention Guide*.
3. SecureW2. *What is DNS Poisoning? How to Prevent DNS Spoofing Attacks*.
4. NIST (National Institute of Standards and Technology). *Secure Domain Name System (DNS) Deployment Guide* (SP 800-81r3).
