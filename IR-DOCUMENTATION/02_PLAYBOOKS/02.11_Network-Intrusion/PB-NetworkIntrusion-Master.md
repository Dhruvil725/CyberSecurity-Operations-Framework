# Playbook: Network Intrusion Incident Response (Master)

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Network Intrusion Incident Response (Master)      |
| Document ID    | IR-PB-NI-001                                                 |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | SOC Manager / Network Security Lead / IR Team Lead           |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 network intrusion incident     |

---

## 2. Purpose

This master playbook defines the end-to-end incident response procedures for network intrusion incidents affecting enterprise and MSSP-managed environments. Network intrusion incidents represent one of the most common and operationally disruptive categories of security events because attackers can leverage compromised network access to move laterally, escalate privileges, exfiltrate sensitive data, and establish long-term persistence across organizational infrastructure.

Unlike many other incident types that begin at the endpoint or identity layer, network intrusions often involve sophisticated techniques such as living-off-the-land movement, encrypted tunneling, protocol abuse, and exploitation of trusted network relationships. These characteristics make network intrusion incidents challenging to detect, scope, and contain without structured and well-coordinated response procedures.

This playbook standardizes:

- Network intrusion detection and triage
- Alert validation and incident qualification
- Investigation across network, endpoint, and log telemetry
- Scoping of attacker movement within the network
- Containment through network segmentation and access control
- Forensic evidence collection from network infrastructure
- Regulatory and breach impact assessment
- Post-incident hardening and detection improvement
- MSSP multi-client network intrusion coordination

---

## 3. Scope

### 3.1 In Scope

This playbook applies to network intrusion incidents involving:

- Unauthorized network access
- Internal network lateral movement
- Network-based exploitation
- Protocol abuse and tunneling
- Firewall and IDS/IPS evasion
- VPN compromise
- Network reconnaissance
- Internal network scanning
- Command and control traffic
- East-west threat movement
- Rogue network devices
- Network segmentation bypass
- Wireless network intrusion
- Network-based data exfiltration

### 3.2 Network Environment Coverage

| Environment | Examples |
|---|---|
| Corporate LAN | Internal office networks |
| Data Center Networks | Server segmentation zones |
| DMZ | Internet-facing service zones |
| VPN | Remote access networks |
| Cloud Networking | VPC, VNET, GCP VPC |
| OT/ICS Adjacent | Networks bordering operational technology |
| Wireless | Corporate and guest wireless networks |
| SD-WAN | Software-defined WAN infrastructure |

### 3.3 Out of Scope

| Scenario | Use Playbook |
|---|---|
| Pure web application attack | 02.8_Web-Application-Attack/ |
| Cloud-only IAM compromise | 02.10_Cloud-Security-Incident/ |
| Ransomware with network spread | 02.1_Ransomware/ |
| DDoS without intrusion | 02.4_DDoS/ |
| Physical security breach | CAT-14-Physical-Security-Incident.md |

---

## 4. Network Intrusion Categories

Network intrusion incidents can manifest in multiple forms. Understanding the category helps responders apply the correct investigation and containment approach.

| Category | Description | Typical Severity |
|---|---|---|
| External to Internal Intrusion | Attacker breaches perimeter and enters internal network | P1/P2 |
| Lateral Movement | Attacker moves between internal systems after initial access | P1/P2 |
| C2 Communication | Malicious outbound communication to attacker infrastructure | P1/P2 |
| Network Reconnaissance | Internal scanning and enumeration | P2/P3 |
| VPN Compromise | Unauthorized VPN access | P1/P2 |
| Segmentation Bypass | Access across network zones without authorization | P1/P2 |
| Protocol Tunneling | Data or C2 tunneled through legitimate protocols | P2 |
| Rogue Device | Unauthorized device connected to internal network | P2/P3 |
| Wireless Intrusion | Unauthorized wireless access | P2/P3 |
| Exfiltration Channel | Network-based data exfiltration detected | P1 |

---

## 5. Severity Classification

| Scenario | Default Severity |
|---|---|
| Active C2 communication confirmed | P1 |
| Lateral movement across critical systems | P1 |
| Perimeter breach with confirmed internal access | P1 |
| Data exfiltration via network channel | P1 |
| VPN compromise with internal access | P1/P2 |
| Network scanning of sensitive segments | P2 |
| Segmentation bypass detected | P2 |
| Suspicious encrypted tunnel detected | P2 |
| Rogue device on internal network | P2/P3 |
| Network anomaly without confirmed intrusion | P3 |
| Informational IDS/IPS alert | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 6. Network Intrusion Response Lifecycle

| Phase | Description | Primary Owner |
|---|---|---|
| Detection and Triage | Alert validation and initial scoping | L1/L2 |
| Investigation | Scope attacker movement and identify affected assets | L2 |
| Forensics | Deep-dive packet analysis and evidence collection | L3 |
| Containment | Network segmentation and access restriction | IR Team / Network Team |
| Eradication | Remove attacker access and close entry points | Network / IR Team |
| Recovery | Restore and validate network integrity | Network Team |
| Post-Incident | PIR, detection engineering, network hardening | IR / Network Security |

---

## 7. Network Intrusion Detection Sources

### 7.1 Network-Based Detection Sources

Effective network intrusion detection relies on a layered monitoring approach across multiple network telemetry sources.

| Source | Purpose |
|---|---|
| IDS/IPS | Signature and anomaly-based intrusion detection |
| Firewall Logs | Perimeter and inter-zone traffic monitoring |
| NetFlow/IPFIX | Network traffic volume and pattern analysis |
| DNS Logs | Command and control and exfiltration detection |
| Proxy Logs | HTTP/HTTPS traffic inspection |
| VPN Logs | Remote access monitoring |
| NDR Platform | Network detection and response |
| Packet Capture | Deep packet analysis |
| DHCP Logs | Rogue device and anomalous host detection |

### 7.2 Endpoint and Host-Based Sources

Network intrusion investigations must correlate network telemetry with host-level evidence.

| Source | Purpose |
|---|---|
| EDR | Process and network connection telemetry |
| Windows Event Logs | Authentication and lateral movement |
| Syslog | Linux and network device activity |
| Authentication Logs | VPN and internal access |
| Active Directory Logs | Lateral movement and credential abuse |

### 7.3 SIEM Correlation

All network intrusion alerts should be correlated within the SIEM against:

- Authentication events
- Endpoint telemetry
- Threat intelligence feeds
- Historical behavioral baselines
- Known malicious IP and domain lists

---

## 8. Core Investigation Areas

Every network intrusion investigation must assess the following areas systematically.

| Investigation Area | Key Questions |
|---|---|
| Entry Point | How did the attacker gain network access? |
| Affected Assets | Which systems were accessed or compromised? |
| Lateral Movement | How did the attacker move within the network? |
| Privilege Escalation | Did the attacker gain elevated access? |
| C2 Communication | Is there ongoing attacker communication? |
| Data Access | Was sensitive data accessed or exfiltrated? |
| Persistence | Did the attacker establish persistence? |
| Dwell Time | How long has the attacker been present? |
| Scope | Which network segments are affected? |
| Impact | What is the operational and data impact? |

---

## 9. Initial Alert Triage Approach

When a network intrusion alert is received, L1 analysts must perform rapid initial triage to determine whether the alert represents a genuine security incident.

The initial triage process should assess:

- Alert source and detection logic
- Affected source and destination IP addresses
- Protocol and port combinations
- Traffic volume and pattern
- Whether the traffic matches known malicious indicators
- Internal asset classification of affected hosts
- Geographic and temporal anomalies
- Correlation with other recent alerts

If initial triage confirms suspicious activity, the incident should be escalated to L2 for full investigation.

---

## 10. Network Investigation Principles

Network intrusion investigations must follow structured principles to ensure completeness and evidence integrity.

### 10.1 Timeline First

Establish an accurate timeline before drawing conclusions. Network intrusions often have extended dwell periods, and early activity may be subtle. Investigators should build the timeline from earliest available evidence and extend backward when possible.

### 10.2 Assume Lateral Movement

Network intrusions rarely remain isolated to a single host. Investigators should always assume lateral movement has occurred and verify through network telemetry before concluding scope is limited.

### 10.3 Preserve Evidence

Network-based evidence is volatile and time-sensitive. Packet captures, NetFlow records, and firewall logs must be preserved before log rotation or system changes occur.

### 10.4 Correlate Across Layers

Network-only investigation is insufficient. Effective network intrusion investigation requires correlation across:

- Network telemetry
- Endpoint activity
- Authentication logs
- Application logs
- Threat intelligence

### 10.5 Protect Investigation Integrity

Avoid alerting the attacker to the investigation. Containment actions should be carefully planned to avoid triggering attacker countermeasures such as evidence destruction.

---

## 11. Escalation Criteria

### 11.1 Escalate to L2 if:

- IDS/IPS alert is confirmed as not a false positive
- Internal scanning activity detected
- Suspicious outbound connection confirmed
- VPN anomaly is confirmed
- Multiple alerts from same source

### 11.2 Escalate to L3 if:

- Lateral movement is confirmed
- C2 communication is confirmed
- Active attacker presence is suspected
- Exploit traffic is detected
- Network forensics required
- Encrypted tunneling confirmed

### 11.3 Escalate to IR Team if:

- Critical system compromise confirmed
- Data exfiltration in progress
- Multiple network segments affected
- APT indicators present
- Attacker has admin-level network access
- Regulatory reporting is likely required

### 11.4 Escalate to Legal and Compliance if:

- Sensitive data access confirmed
- Customer data exposure suspected
- Regulated data in scope
- Law enforcement engagement required

---

## 12. Containment Principles

Network containment must balance operational continuity with security risk reduction. Aggressive containment that disrupts business-critical services requires executive approval.

Core containment approaches include:

- Blocking attacker IP addresses at perimeter firewall
- Isolating compromised network segments
- Disabling compromised VPN accounts
- Blocking malicious domains at DNS and proxy
- Restricting lateral movement paths
- Deploying network ACLs to quarantine affected hosts
- Suspending rogue device network access
- Blocking protocol tunneling channels

Reference:
`02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Containment.md`

---

## 13. Data Breach Trigger Assessment

Network intrusions frequently result in data access and exfiltration. Responders must assess breach risk throughout the investigation.

| Question | If YES → Action |
|---|---|
| Was sensitive data accessible from compromised systems? | Activate Data Breach playbook |
| Was outbound data transfer detected? | Assess exfiltration volume immediately |
| Did attacker access database servers? | Engage Legal/Compliance immediately |
| Was customer data in scope of compromise? | Activate breach notification procedures |
| Did attacker access file shares with sensitive content? | Scope data exposure immediately |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`

---

## 14. MSSP Multi-Client Considerations

For MSSP-managed environments, network intrusion incidents require additional coordination.

- Multiple clients may share network management infrastructure
- Cross-tenant evidence segregation is mandatory
- Shared network monitoring infrastructure increases blast radius
- Client notification timing must follow contractual SLA obligations
- Network isolation actions affecting multiple clients require executive approval

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

## 15. Network Forensics Overview

Network forensic evidence is time-sensitive and must be collected early in the investigation process.

### 15.1 Evidence Types

| Evidence Type | Examples |
|---|---|
| Packet captures | Full packet data from intrusion period |
| NetFlow records | Traffic volume and connection metadata |
| Firewall logs | Allow and deny decisions |
| IDS/IPS logs | Signature matches and anomalies |
| DNS logs | Queries and responses |
| Proxy logs | HTTP/S traffic |
| VPN logs | Connection and authentication records |
| DHCP logs | IP assignment history |

### 15.2 Evidence Preservation Rules

- Collect and export logs before rotation
- Preserve packet captures in original format
- Hash all forensic exports
- Maintain chain-of-custody documentation
- Record timestamps in UTC

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Common Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|---|---|---|
| Blocking attacker IP without investigation | Attacker pivots; investigation loses visibility | Monitor first; block after scope is understood |
| Failing to capture packets early | Critical evidence lost | Initiate packet capture immediately on detection |
| Assuming single host compromise | Underestimating scope | Always investigate lateral movement |
| Not reviewing DNS logs | C2 and exfiltration missed | Include DNS in every investigation |
| Terminating connections before logging | Evidence destroyed | Preserve logs before terminating sessions |
| Ignoring encrypted traffic | Tunneling and C2 missed | Analyze SSL/TLS metadata and anomalies |
| Failing to check VPN logs | Entry point missed | Always review VPN in external intrusion |

---

## 17. Related Documents

| Document | Path |
|---|---|
| Network Intrusion L1 Triage | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L1-Triage.md` |
| Network Intrusion L2 Investigation | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L2-Investigation.md` |
| Network Intrusion L3 Forensics | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L3-Forensics.md` |
| Network Intrusion Containment | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Containment.md` |
| Network Intrusion MITRE Mapping | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-MITRE-Mapping.md` |
| Data Breach Playbooks | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` |
| Cloud Security Playbooks | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 21-May-2026 | SOC Manager / Network Security Lead / IR Team Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**