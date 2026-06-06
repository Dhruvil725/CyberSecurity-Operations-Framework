# Playbook: Network Intrusion – L2 Investigation

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Network Intrusion (L2 Investigation)              |
| Document ID    | IR-PB-NI-003                                                 |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | L2 SOC Lead / Network Security Lead                          |
| Approved By    | IR Team Lead                                                 |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 network intrusion incident     |

---

## 2. Purpose

This document defines the Level 2 (L2) investigation procedures for network intrusion incidents escalated from L1 triage.

Network intrusion investigations at L2 differ from basic alert triage because:

- Attackers often use legitimate protocols and credentials
- Intrusions may involve multi-stage lateral movement
- C2 communication may blend with normal traffic
- Network telemetry must be correlated with endpoint and authentication logs
- Evidence may be distributed across firewall, IDS, DNS, proxy, EDR, and identity platforms
- Attacker dwell time may span days or weeks before detection

L2 objectives:

- Confirm whether intrusion occurred
- Identify initial access vector
- Determine full scope of affected systems
- Identify lateral movement paths
- Assess C2 activity and persistence
- Determine data access or exfiltration
- Build prioritized containment recommendations
- Escalate to L3 or IR Team when required

L2 must produce:

- Technically defensible investigation summary
- Confirmed incident classification
- Complete asset scope mapping
- Structured UTC timeline
- Clear impact assessment
- Prioritized containment plan
- Evidence references for every major finding

---

## 3. Scope

Applies to investigation of:

- External perimeter intrusions
- Internal lateral movement
- VPN compromise
- IDS/IPS confirmed exploit traffic
- Suspicious outbound connections (C2)
- Internal scanning and reconnaissance
- Protocol tunneling (DNS/HTTP/SSL)
- Segmentation bypass
- Rogue internal devices
- Multi-zone network compromise
- MSSP client network incidents

Includes:

- Corporate LAN
- Data center network segments
- DMZ zones
- VPN access networks
- Cloud-connected networks
- Wireless networks
- Hybrid cloud/on-prem integrated networks

---

## 4. Preconditions (Inputs from L1)

Before L2 begins, confirm the ticket includes:

| Required Input              | Minimum Content                                      |
| --------------------------- | ---------------------------------------------------- |
| Alert source                | IDS / Firewall / SIEM / NDR                         |
| Source IP address           | Internal or external                                 |
| Destination IP address      | Internal asset identified                            |
| Protocol and port           | Yes                                                  |
| Timestamp                   | UTC                                                  |
| Asset classification        | Criticality and business owner                       |
| Initial severity            | P1–P4 with rationale                                 |
| Threat intelligence context | Indicator enrichment results                         |
| Initial evidence references | Log extracts or SIEM event references                |

Reference:
`02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L1-Triage.md`

---

## 5. L2 Required Outputs

L2 must provide the following:

| Output                          | Required Detail                                      |
| -------------------------------- | ---------------------------------------------------- |
| Confirmed incident status       | Confirmed / Likely / Not confirmed                   |
| Entry point identification      | Exploit / VPN / Credential / Other                   |
| Affected asset inventory        | All compromised or accessed systems                  |
| Lateral movement assessment     | Movement paths and authentication evidence           |
| C2 assessment                   | Ongoing or historical attacker communication         |
| Data access/exfiltration status | Confirmed / Likely / Not confirmed                   |
| Persistence assessment          | Accounts, services, tasks, tools                     |
| Timeline                        | UTC timeline with evidence references                |
| Containment recommendations     | Prioritized actions                                  |
| Escalation decision             | L3 / IR Team requirement                             |
| Evidence references             | All findings linked to evidence                      |

---

## 6. Investigation Workflow Overview

| Phase   | Goal                                                  | Key Output                     |
| ------- | ----------------------------------------------------- | ------------------------------ |
| Phase 1 | Confirm intrusion                                     | Confirmed status               |
| Phase 2 | Identify entry point                                  | Entry vector                   |
| Phase 3 | Scope affected systems                                | Asset inventory                |
| Phase 4 | Analyze lateral movement                              | Movement map                   |
| Phase 5 | Investigate C2 communication                          | C2 confirmation status         |
| Phase 6 | Assess data access and exfiltration                   | Data exposure status           |
| Phase 7 | Identify persistence                                  | Persistence mechanisms         |
| Phase 8 | Build timeline                                        | Structured UTC timeline        |
| Phase 9 | Containment recommendations and escalation decision   | Action plan                    |

---

# 7. Phase 1 – Confirm Intrusion

L2 must determine whether the alert represents confirmed malicious activity or an advanced false positive.

---

## 7.1 Intrusion Confidence Levels

| Level         | Meaning                                                  | Evidence Required                                  |
| ------------- | -------------------------------------------------------- | -------------------------------------------------- |
| Confirmed     | Unauthorized access or malicious activity confirmed      | Log correlation or exploit evidence                |
| Highly Likely | Strong indicators of compromise                          | Multiple corroborated indicators                   |
| Possible      | Suspicious behavior but inconclusive                     | Single moderate-confidence indicator               |
| Not Confirmed | Alert determined benign                                  | Evidence disproves malicious intent                |

---

## 7.2 Immediate High-Risk Indicators

If any of the following are confirmed, escalate severity immediately:

| Indicator                                         | Risk Level |
| ------------------------------------------------- | ---------- |
| Confirmed C2 beaconing                            | Critical   |
| Domain controller access                          | Critical   |
| VPN compromise with internal access               | High       |
| Internal lateral movement using admin accounts    | Critical   |
| Exploit traffic followed by successful access     | High       |
| Large outbound data transfer                      | Critical   |
| IDS exploit signature with confirmed execution    | High       |
| Pass-the-Hash or Pass-the-Ticket evidence         | Critical   |
| RDP lateral movement from workstation to server   | High       |
| Multiple internal segments affected               | Critical   |

---

# 8. Phase 2 – Identify Entry Point

L2 must determine how the attacker gained network access.

---

## 8.1 Common Entry Vectors

| Entry Type            | Evidence Source                                      |
| --------------------- | ---------------------------------------------------- |
| Exploited service     | IDS + firewall logs                                  |
| VPN compromise        | VPN logs + authentication logs                       |
| Phishing foothold     | EDR + email logs                                     |
| Web server compromise | Web logs + IDS                                       |
| Credential reuse      | Authentication logs                                  |
| Rogue device          | DHCP logs + NAC logs                                 |
| Wireless intrusion    | Wireless controller logs                             |

---

## 8.2 Entry Point Investigation Questions

| Question                                                     | Required Output                      |
| ------------------------------------------------------------ | ------------------------------------ |
| Was inbound traffic allowed or blocked?                      | Yes/No                               |
| Was authentication successful?                               | Yes/No                               |
| Which system was first accessed?                             | Hostname/IP                          |
| What vulnerability or credential was used?                   | Exploit/Credential                   |
| Did attacker escalate immediately after access?              | Yes/No                               |

---

# 9. Phase 3 – Scope Affected Systems

L2 must identify all systems touched during the intrusion.

---

## 9.1 Scope Assessment Table

| Hostname/IP | Role | Segment | Accessed? | Authenticated? | Evidence Ref |
| ------------ | ---- | ------- | ---------- | -------------- | ------------ |
|              |      |         |            |                |              |

---

## 9.2 Scope Activities

- Review NetFlow for internal connections from compromised host
- Identify all unique destination IPs contacted
- Correlate authentication logs for internal logins
- Check RDP, SMB, WinRM connections
- Review firewall logs for east-west traffic
- Map network zones accessed
- Check whether restricted VLANs were accessed

---

# 10. Phase 4 – Lateral Movement Analysis

Network intrusions often expand beyond initial host.

---

## 10.1 Lateral Movement Indicators

| Indicator                              | Meaning                             |
| -------------------------------------- | ----------------------------------- |
| SMB access to admin shares             | Potential lateral movement          |
| RDP from workstation to server         | Unauthorized access attempt         |
| Kerberos service ticket anomalies      | Credential abuse                    |
| NTLM authentication spike              | Pass-the-Hash attempt               |
| WMI remote execution                   | Remote command execution            |
| PsExec activity                        | Tool-based lateral movement         |
| Scheduled task created remotely        | Persistence/lateral movement        |

---

## 10.2 Required Lateral Movement Assessment

| Question                                              | Answer |
| ----------------------------------------------------- | ------ |
| Were admin credentials used?                          |        |
| Was domain controller accessed?                       |        |
| Were service accounts abused?                         |        |
| Were new systems accessed post-initial compromise?    |        |

---

# 11. Phase 5 – C2 Communication Investigation

C2 detection is a high-priority objective.

---

## 11.1 C2 Indicators

| Indicator                              | Meaning                             |
| -------------------------------------- | ----------------------------------- |
| Regular beacon intervals               | Automated callback                  |
| Consistent packet size                 | Structured C2 traffic               |
| High entropy DNS queries               | DGA usage                           |
| Outbound SSL to unknown IP             | Encrypted C2                        |
| Proxy bypass attempts                  | Evasion attempt                     |
| Unusual HTTP user agent                | Tool fingerprint                    |

---

## 11.2 C2 Assessment Table

| Host | Destination | Port | Frequency | TI Status | Evidence Ref |
| ---- | ------------ | ---- | --------- | ---------- | ------------ |
|      |              |      |           |            |              |

---

# 12. Phase 6 – Data Access and Exfiltration

Determine whether sensitive data was accessed or exfiltrated.

---

## 12.1 Data Access Checklist

| Check                                      | Why Important                        |
| ------------------------------------------ | ------------------------------------ |
| File server access logs                    | Identify sensitive file access       |
| Database connection logs                   | Structured data access               |
| Proxy upload logs                          | Outbound transfer review             |
| NetFlow large transfer analysis            | Volume anomaly detection             |
| DLP alerts                                 | Data protection confirmation         |
| Cloud storage access logs                  | Hybrid environment exposure          |

---

## 12.2 Exfiltration Assessment Table

| Host | Destination | Bytes Out | Duration | Confirmed? | Evidence Ref |
| ---- | ------------ | --------- | -------- | ---------- | ------------ |
|      |              |           |          |            |              |

If confirmed or highly likely:
- Activate Data Breach playbook
- Notify SOC Lead immediately

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`

---

# 13. Phase 7 – Persistence Investigation

---

## 13.1 Persistence Indicators

| Mechanism                               | Evidence Source                     |
| --------------------------------------- | ----------------------------------- |
| Scheduled tasks                          | Event ID 4698                       |
| New services installed                   | Event ID 7045                       |
| Registry run keys                        | Registry logs                       |
| New user accounts                        | Event ID 4720                       |
| Group membership changes                 | Event ID 4732                       |
| Unauthorized SSH keys                    | Linux auth logs                     |
| Startup folder modifications             | File integrity monitoring           |

---

# 14. Phase 8 – Timeline Reconstruction

All investigations must produce a structured UTC timeline.

---

## 14.1 Timeline Anchors

| Event | Source |
|-------|--------|
| Initial alert | IDS/SIEM |
| First inbound connection | Firewall logs |
| First successful login | Authentication logs |
| Lateral movement event | Windows logs |
| C2 initiation | Proxy/DNS logs |
| Containment action | Change logs |

---

## 14.2 Timeline Table

| Time (UTC) | Host | Event | Source | Evidence Ref |
|------------|------|-------|--------|--------------|
|            |      |       |        |              |

---

# 15. Phase 9 – Containment Recommendations

---

## 15.1 Containment Matrix

| Finding                         | Recommended Action                     | Owner          | Approval |
| ------------------------------ | -------------------------------------- | -------------- | -------- |
| Confirmed C2                   | Block IP/domain immediately            | Network Team  | SOC Lead |
| Compromised host               | Network isolate                        | Network Team  | SOC Lead |
| Admin credential abuse         | Reset credentials                      | IAM Team      | SOC Lead |
| VPN compromise                 | Disable account/session                | IAM Team      | SOC Lead |
| Domain controller access       | Activate IR Team                       | IR Team       | CISO     |
| Data exfiltration              | Block egress + activate breach process | IR Team       | CISO     |

---

## 15.2 High-Risk Containment Actions

| Action                            | Risk |
| ---------------------------------- | ---- |
| Blocking entire subnet             | Business disruption |
| Shutting down domain controller    | Major outage |
| Resetting all privileged accounts  | Operational impact |
| Disabling VPN globally             | Remote workforce impact |

---

# 16. Escalation Decision

---

## 16.1 Escalate to L3 if:

| Condition                               | Reason                               |
| --------------------------------------- | ------------------------------------ |
| Advanced malware detected               | Reverse engineering required         |
| Memory analysis required                | Volatile artifact recovery           |
| Packet-level deep forensics required    | PCAP analysis needed                 |
| APT indicators identified               | Attribution assessment required      |
| Domain controller compromise suspected  | Advanced investigation required      |

---

## 16.2 Escalate to IR Team if:

| Condition                               | Reason                               |
| --------------------------------------- | ------------------------------------ |
| Critical infrastructure compromise      | Crisis-level incident                |
| Confirmed data exfiltration             | Legal/regulatory impact              |
| Multi-segment compromise                | Enterprise-wide risk                 |
| Active attacker presence confirmed      | Major incident                       |
| Regulatory reporting likely             | Compliance obligation                |

---

# 17. Documentation Requirements

Before handoff or closure, confirm:

| Requirement                                      | Status |
| ------------------------------------------------ | ------ |
| Entry point identified                           | ☐      |
| Scope completed                                  | ☐      |
| Lateral movement assessed                        | ☐      |
| C2 status confirmed                              | ☐      |
| Data exposure assessed                           | ☐      |
| Timeline completed                               | ☐      |
| Containment recommendations documented           | ☐      |
| Escalation decision documented                   | ☐      |
| Evidence preserved                               | ☐      |

---

## 18. MSSP Client Handling Notes

For MSSP environments:

- Segregate client evidence
- Follow client-specific SLA
- Notify client contacts per escalation matrix
- Obtain client approval for high-impact containment
- Escalate to SDM for P1/P2 incidents

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

## 19. Related Documents

| Document | Path |
|----------|------|
| Network Intrusion Master | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md` |
| Network Intrusion L1 | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L1-Triage.md` |
| Network Intrusion L3 | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L3-Forensics.md` |
| Network Intrusion Containment | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Containment.md` |
| Network Intrusion MITRE Mapping | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-MITRE-Mapping.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 20. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | L2 SOC Lead / Network Security Lead | Initial version |

---

## 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**