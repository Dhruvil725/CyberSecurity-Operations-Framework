# Playbook: DDoS – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – DDoS (MITRE ATT&CK Mapping) |
| Document ID | IR-PB-DDoS-006 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | Threat Intelligence Lead / Network Security Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after major DDoS incidents |

---

## 2. Purpose

This document maps Distributed Denial of Service (DDoS) attack activity
to the MITRE ATT&CK framework.

The objective is to:
- standardize DDoS investigation documentation
- improve attack classification consistency
- support threat hunting and detection engineering
- improve reporting quality
- align DDoS analysis with ATT&CK terminology
- support intelligence-driven mitigation

This mapping supports:
- SOC investigations
- network analysis
- DDoS response activities
- mitigation tuning
- attack trend analysis
- executive and technical reporting

---

## 3. Scope

Applies to:
- volumetric DDoS attacks
- protocol-based attacks
- application-layer attacks
- reflection/amplification attacks
- botnet-driven campaigns
- hybrid DDoS operations
- extortion-driven DDoS threats

Includes:
- attack infrastructure
- traffic generation techniques
- protocol abuse
- application abuse
- attack coordination indicators

---

## 4. How to Use This Mapping

During DDoS investigations:
1. Identify attack characteristics.
2. Map attack behavior to ATT&CK techniques.
3. Document:
   - ATT&CK Technique ID
   - Technique Name
   - Evidence Source
   - Confidence Level
4. Use mappings to:
   - improve mitigations
   - improve detections
   - support threat intelligence
   - identify recurring campaigns
   - improve attack classification

---

## 5. High-Level DDoS Attack Lifecycle

Typical DDoS operations follow this progression:

1. Resource Development
2. Reconnaissance
3. Infrastructure Preparation
4. Traffic Generation
5. Delivery and Saturation
6. Persistence of Attack
7. Service Degradation or Outage
8. Adaptation and Evasion

Not all attacks include every stage.

---

# 6. MITRE ATT&CK Mapping Table

| Tactic | Technique ID | Technique Name | Common DDoS Evidence | Primary Data Sources |
|--------|--------------|----------------|----------------------|----------------------|
| Reconnaissance | T1595 | Active Scanning | port scans before attack | firewall logs |
| Reconnaissance | T1590 | Gather Victim Network Information | DNS and ASN research | DNS logs |
| Resource Development | T1583 | Acquire Infrastructure | VPS/cloud infrastructure | WHOIS, TI feeds |
| Resource Development | T1584 | Compromise Infrastructure | compromised servers used as bots | TI reports |
| Resource Development | T1587 | Develop Capabilities | custom DDoS tools/scripts | malware analysis |
| Initial Access | T1189 | Drive-by Compromise | botnet infection vectors | malware telemetry |
| Initial Access | T1566 | Phishing | botnet malware delivery | email telemetry |
| Execution | T1059 | Command and Scripting Interpreter | attack scripts | shell logs |
| Persistence | T1098 | Account Manipulation | compromised infrastructure persistence | cloud/IAM logs |
| Persistence | T1053 | Scheduled Task/Job | botnet persistence | endpoint telemetry |
| Defense Evasion | T1562 | Impair Defenses | disabling protections | firewall/WAF logs |
| Defense Evasion | T1036 | Masquerading | fake user-agents | HTTP logs |
| Discovery | T1046 | Network Service Discovery | target service scanning | IDS/IPS |
| Discovery | T1016 | System Network Configuration Discovery | routing or network discovery | endpoint logs |
| Collection | T1005 | Data from Local System | bot configuration collection | malware analysis |
| Command and Control | T1071 | Application Layer Protocol | HTTP/S-based botnet traffic | proxy logs |
| Command and Control | T1095 | Non-Application Layer Protocol | raw UDP/TCP floods | NetFlow |
| Impact | T1498 | Network Denial of Service | bandwidth saturation | network telemetry |
| Impact | T1499 | Endpoint Denial of Service | application/resource exhaustion | server metrics |
| Impact | T1498.001 | Direct Network Flood | direct traffic flood | firewall logs |
| Impact | T1498.002 | Reflection Amplification | DNS/NTP amplification | NetFlow, DNS logs |
| Impact | T1499.001 | OS Exhaustion Flood | SYN floods | firewall/session logs |
| Impact | T1499.002 | Service Exhaustion Flood | HTTP/API floods | WAF logs |

---

# 7. Volumetric Attack Mapping

Volumetric attacks focus on saturating bandwidth.

---

## 7.1 Common Volumetric Techniques

| ATT&CK Technique | Evidence | Detection Opportunity |
|------------------|----------|-----------------------|
| T1498 Direct Network Flood | Gbps-level traffic spikes | NetFlow monitoring |
| T1498.002 Reflection Amplification | DNS/NTP response floods | Protocol monitoring |
| T1071 Application Layer Protocol | HTTP flood traffic | WAF analysis |

---

## 7.2 Reflection/Amplification Mapping

| Protocol | ATT&CK Context | Common Evidence |
|-----------|----------------|----------------|
| DNS | Reflection attack | DNS response spikes |
| NTP | Amplification attack | Monlist traffic |
| Memcached | High amplification | UDP flood |
| SSDP | Reflection | UPnP traffic |

---

# 8. Protocol Attack Mapping

Protocol attacks exhaust infrastructure resources.

---

## 8.1 Common Protocol Techniques

| ATT&CK Technique | Evidence | Detection |
|------------------|----------|----------|
| T1499 Endpoint DoS | Firewall session exhaustion | Firewall metrics |
| T1499.001 OS Exhaustion Flood | SYN flood | Half-open sessions |
| T1095 Non-App Protocol | Raw packet floods | NetFlow |

---

## 8.2 Protocol Exhaustion Indicators

| Indicator | Meaning |
|-----------|---------|
| SYN backlog increase | SYN flood |
| High packet rate | Protocol attack |
| Connection exhaustion | Firewall overload |
| Stateful inspection failures | Resource exhaustion |

---

# 9. Application Layer Attack Mapping

Application-layer attacks target backend applications and APIs.

---

## 9.1 HTTP/HTTPS Flood Mapping

| ATT&CK Technique | Common Evidence | Detection |
|------------------|----------------|----------|
| T1499.002 Service Exhaustion Flood | excessive HTTP requests | WAF logs |
| T1071 Application Layer Protocol | HTTP bot traffic | proxy logs |
| T1036 Masquerading | fake user-agents | HTTP analysis |

---

## 9.2 API Abuse Mapping

| ATT&CK Technique | Evidence |
|------------------|----------|
| T1499.002 Service Exhaustion | excessive API calls |
| T1071 Application Layer Protocol | API request floods |

---

## 9.3 Bot Behavior Indicators

| Indicator | Meaning |
|-----------|---------|
| No cookie persistence | Automation |
| Repetitive requests | Bot behavior |
| Invalid browser behavior | Scripted traffic |
| High concurrency | Distributed bots |

---

# 10. Botnet Infrastructure Mapping

Botnets are commonly used for DDoS campaigns.

---

## 10.1 Botnet Indicators

| Indicator | Meaning |
|-----------|---------|
| Large source IP diversity | Distributed attack |
| VPS/cloud provider traffic | Hosted attack nodes |
| Geographic randomness | Botnet distribution |
| Shared user-agents | Bot coordination |

---

## 10.2 ATT&CK Mapping for Botnets

| ATT&CK Technique | Evidence |
|------------------|----------|
| T1583 Acquire Infrastructure | cloud/VPS servers |
| T1584 Compromise Infrastructure | compromised systems |
| T1071 Application Layer Protocol | HTTP-based C2 |
| T1095 Non-App Protocol | custom botnet traffic |

---

# 11. Attack Adaptation and Evasion Mapping

Attackers frequently change vectors during mitigation.

---

## 11.1 Adaptation Techniques

| ATT&CK Technique | Example |
|------------------|---------|
| T1036 Masquerading | changing user-agents |
| T1562 Impair Defenses | bypassing WAF rules |
| T1498 Direct Network Flood | shifting protocols |

---

## 11.2 Evasion Indicators

| Indicator | Meaning |
|-----------|---------|
| Switching attack vectors | Adaptive attacker |
| Changing source regions | Geo-block evasion |
| Rotating domains/IPs | Dynamic infrastructure |
| Low-and-slow requests | WAF evasion |

---

# 12. Technique Confirmation Guidance

Use confidence levels consistently.

| Confidence Level | Meaning | Documentation Requirement |
|------------------|---------|---------------------------|
| Confirmed | Direct evidence available | Include metrics and logs |
| Likely | Strong indicators | Include supporting evidence |
| Possible | Weak indicators | Further investigation required |

---

# 13. Detection and Hunting Recommendations

---

## 13.1 Network Monitoring Recommendations

| Monitoring Area | Purpose |
|-----------------|---------|
| Bandwidth anomalies | Detect volumetric floods |
| Packet rate anomalies | Detect protocol floods |
| ASN concentration | Detect attack infrastructure |
| DNS anomalies | Detect reflection attacks |

---

## 13.2 Application Monitoring Recommendations

| Monitoring Area | Purpose |
|-----------------|---------|
| Request rate spikes | Detect L7 floods |
| Login/API abuse | Detect targeted attacks |
| Error rate increases | Detect service degradation |
| Session anomalies | Detect bot behavior |

---

## 13.3 Threat Hunting Recommendations

| Hunt Area | Purpose |
|-----------|---------|
| Repeated ASN patterns | Recurring campaigns |
| User-agent anomalies | Bot detection |
| Reflection traffic | Amplification detection |
| Historical attack patterns | Attribution support |

---

# 14. Detection Engineering Recommendations

Every DDoS incident should improve monitoring and mitigation.

---

## 14.1 Recommended Improvements

| Improvement | Purpose |
|-------------|---------|
| New rate-limiting rules | Reduce future impact |
| WAF tuning | Improve filtering |
| NetFlow anomaly detection | Faster identification |
| ASN-based alerts | Botnet detection |
| API abuse monitoring | L7 visibility |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 15. Reporting Requirements

The final report should include:
- mapped ATT&CK techniques
- attack type classification
- peak traffic metrics
- mitigation effectiveness
- infrastructure impact
- lessons learned
- recommended improvements

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

# 16. MSSP Client Handling Notes

For MSSP-managed environments:
- maintain client-specific ATT&CK mappings
- anonymize cross-client attack intelligence
- maintain client traffic segregation
- provide client-specific technical summaries

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 17. Related Documents

| Document | Path |
|---------|------|
| DDoS Master | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Master.md` |
| DDoS L1 Triage | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L1-Triage.md` |
| DDoS L2 Investigation | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L2-Investigation.md` |
| DDoS Mitigation Steps | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Mitigation-Steps.md` |
| ISP Coordination | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-ISP-Coordination.md` |
| MITRE ATT&CK Quick Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATTCK-Quick-Reference.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | Threat Intelligence Lead / Network Security Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document