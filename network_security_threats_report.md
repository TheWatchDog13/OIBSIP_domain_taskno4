# Network Security Threats Report

## Executive Summary
Modern networks face a handful of recurring, high-impact threats. This report explains how Denial-of-Service (DoS/DDoS), Man-in-the-Middle (MITM), and spoofing attacks work; the damage they cause; real-world incidents; and practical, prioritized controls to prevent and detect them.

---

## 1) Denial-of-Service (DoS/DDoS)

### What it is
A DoS attack attempts to make a service unavailable by overwhelming resources (bandwidth, CPU, memory, state tables). Distributed DoS (DDoS) amplifies the effect by coordinating traffic from many compromised devices (bots).

### How it works
1. Attacker builds/leases a botnet (often IoT devices with weak credentials).
2. Bots send massive traffic or reflected traffic.
3. Target’s resources saturate or crash.

### Impact
- Outage and degraded performance.
- Collateral congestion upstream.
- Incident response costs and reputational damage.

### Real-world examples
- Dyn DNS (Oct 21, 2016) disrupted access to major websites via Mirai botnet.
- GitHub (Feb 28, 2018) hit by a 1.35 Tbps memcached amplification attack.

### Mitigations
1. Upstream DDoS protection (scrubbing, anycast).
2. Edge hardening: SYN cookies, rate-limits, ACLs.
3. Application resilience: caching, request queuing, autoscaling.
4. Reduce amplification: disable open UDP services, ingress filtering.
5. Run DDoS drills and maintain playbooks.

---

## 2) Man-in-the-Middle (MITM)

### What it is
An adversary intercepts and possibly modifies traffic between two parties.

### How it works
- Local LAN/Wi-Fi: ARP spoofing or rogue AP.
- TLS subversion: fraudulent certificates.
- Protocol flaws: handshake manipulation.

### Impact
- Credential/session theft.
- Data exfiltration or tampering.

### Real-world examples
- DigiNotar CA compromise (2011) allowed interception of Gmail traffic in Iran.
- Lenovo Superfish (2014-2015) installed root certificates enabling HTTPS spoofing.
- KRACK (2017) allowed replay/forging packets on WPA2.

### Mitigations
1. Enforce modern TLS, HSTS, certificate pinning.
2. PKI hygiene: CT monitoring, automated cert rotation.
3. LAN and Wi-Fi defenses: 802.1X/WPA3, DHCP snooping, Dynamic ARP Inspection.
4. VPN use on untrusted networks.
5. Train users to respond to certificate warnings.

---

## 3) Spoofing (IP, ARP, DNS, Email, BGP)

### What it is
Forging identity or data to appear trusted. Types include:
- IP spoofing
- ARP spoofing
- DNS spoofing/cache poisoning
- Email spoofing
- BGP route hijacking

### Real-world examples
- Kaminsky DNS cache poisoning (2008)
- YouTube BGP hijack (2008)
- Amazon Route 53/MyEtherWallet BGP hijack (2018)

### How it works & impact
- IP/Reflection: enable DDoS floods.
- ARP: LAN MITM or DoS.
- DNS: redirect users to attacker servers.
- Email: phishing/BEC attacks.
- BGP: traffic diversion or blackholing.

### Mitigations
1. Anti-spoofing at the edge (BCP 38/84).
2. DNS security: DNSSEC validation, restrict recursion.
3. LAN hardening: DHCP snooping, Dynamic ARP Inspection.
4. Email authentication: SPF, DKIM, DMARC.
5. BGP hygiene: prefix filtering, RPKI validation.
6. Close unnecessary UDP services and rate-limit reflectors.

---

## Cross-cutting Preventive Measures
- Asset & exposure management.
- Network architecture: layered defenses, segmented VLANs.
- Zero Trust principles: mutual TLS, least privilege.
- Monitoring/telemetry: NetFlow, DNS logs, TLS/cert telemetry.
- Secure configurations & patching.
- Incident response readiness and tabletop exercises.
- User training on phishing and TLS warnings.

---

## Quick Reference Matrix
| Threat | Primary vector | Typical impact | Highest-value controls |
|---|---|---|---|
| DoS/DDoS | Volumetric floods; reflection/amplification | Outage, revenue loss | Upstream scrubbing, anycast, edge rate-limits, app resilience |
| MITM | ARP/Wi-Fi, rogue APs, PKI abuse, protocol flaws | Credential/session theft, data tampering | Modern TLS + HSTS, 802.1X/WPA3, CT monitoring, DAI/port security, VPN |
| Spoofing | Forged identities/data | Redirection, phishing, DDoS, traffic hijack | BCP38/84, DNSSEC, DAI, SPF/DKIM/DMARC, RPKI/ROV |

---

## Actionable Next Steps
1. Validate ISP DDoS plan and run drills.
2. Enforce HSTS and audit certificate issuance.
3. Enable DNSSEC validation; publish SPF/DKIM/DMARC.
4. Roll out DHCP snooping and Dynamic ARP Inspection.
5. Confirm RPKI ROV and prefix filters with transit providers.

