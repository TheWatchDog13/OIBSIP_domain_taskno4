# Network Security Threats Report

## Executive Summary
This report provides a structured overview of common network security threats and effective countermeasures. It covers Denial-of-Service (DoS/DDoS), Man-in-the-Middle (MITM), and spoofing attacks, explaining how they operate, their potential impact, real-world incidents, and recommended mitigations.

---

## 1) Denial-of-Service (DoS/DDoS)

### Overview
DoS attacks aim to make a service unavailable by overwhelming its resources. Distributed DoS (DDoS) uses multiple compromised devices to amplify the attack.

### Mechanism
- Creation or leasing of a botnet.
- Bots send high-volume traffic to the target.
- Target's resources (bandwidth, CPU, memory) become exhausted.

### Impact
- Service outages and degraded performance.
- Potential revenue loss and reputational damage.

### Real-World Examples
- Dyn DNS (2016) disrupted access to major websites via Mirai botnet.
- GitHub (2018) faced a 1.35 Tbps memcached amplification attack.

### Mitigation Measures
- Deploy upstream DDoS protection and scrubbing services.
- Harden network edges using rate-limits and ACLs.
- Enhance application resilience with caching and autoscaling.
- Disable open UDP services and implement ingress filtering.
- Conduct DDoS drills and maintain response playbooks.

---

## 2) Man-in-the-Middle (MITM)

### Overview
MITM attacks intercept and potentially modify communication between two parties to steal data or credentials.

### Mechanism
- ARP spoofing or rogue Wi-Fi access points.
- Fraudulent TLS certificates.
- Exploiting protocol weaknesses.

### Impact
- Credential theft and session hijacking.
- Data manipulation and loss of integrity.

### Real-World Examples
- DigiNotar CA breach (2011) affected Gmail users in Iran.
- Lenovo Superfish (2014-2015) installed root certificates enabling HTTPS interception.
- KRACK (2017) WPA2 vulnerability allowed packet replay.

### Mitigation Measures
- Enforce modern TLS standards, HSTS, and certificate pinning.
- Monitor PKI and certificate issuance.
- Implement 802.1X/WPA3 and LAN protections like DHCP snooping and Dynamic ARP Inspection.
- Use VPNs on untrusted networks.
- Train users to respond to certificate warnings.

---

## 3) Spoofing (IP, ARP, DNS, Email, BGP)

### Overview
Spoofing involves forging identity or data to appear legitimate, facilitating attacks like phishing, DDoS, or traffic hijacking.

### Mechanism
- IP spoofing for reflection/amplification DDoS.
- ARP spoofing for LAN interception.
- DNS spoofing to redirect traffic.
- Email spoofing for phishing or BEC attacks.
- BGP route hijacking to divert network traffic.

### Real-World Examples
- Kaminsky DNS cache poisoning (2008).
- YouTube BGP hijack (2008).
- Amazon Route 53/MyEtherWallet BGP hijack (2018).

### Mitigation Measures
- Apply anti-spoofing filters (BCP38/84).
- Secure DNS with DNSSEC and restrict recursion.
- Implement LAN hardening measures (DHCP snooping, Dynamic ARP Inspection).
- Deploy email authentication (SPF, DKIM, DMARC).
- Ensure BGP prefix filtering and RPKI validation.
- Close unnecessary UDP services and rate-limit reflectors.

---

## Cross-Cutting Preventive Measures
- Maintain asset and exposure inventories.
- Adopt layered network defenses and VLAN segmentation.
- Implement Zero Trust principles: mutual TLS and least privilege.
- Monitor network activity: NetFlow, DNS logs, TLS telemetry.
- Keep systems patched and configured securely.
- Prepare incident response plans and conduct tabletop exercises.
- Educate users on phishing risks and TLS warnings.

---

## Quick Reference Matrix
| Threat | Primary Vector | Typical Impact | Key Controls |
|---|---|---|---|
| DoS/DDoS | Volumetric floods, reflection/amplification | Service outage, revenue loss | Upstream scrubbing, edge rate-limits, app resilience |
| MITM | ARP/Wi-Fi, rogue APs, PKI abuse, protocol flaws | Credential theft, data tampering | Modern TLS, HSTS, 802.1X/WPA3, certificate monitoring, VPN |
| Spoofing | Forged identities/data | Traffic diversion, phishing, DDoS | BCP38/84, DNSSEC, LAN protections, SPF/DKIM/DMARC, RPKI |

---

## Recommended Next Steps
1. Validate ISP DDoS response plan and run drills.
2. Enforce HSTS and monitor certificate issuance.
3. Enable DNSSEC validation and deploy SPF/DKIM/DMARC policies.
4. Implement DHCP snooping and Dynamic ARP Inspection on network switches.
5. Verify RPKI ROV and prefix filtering with transit providers.

