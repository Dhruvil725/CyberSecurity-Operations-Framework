# Playbook: Network Intrusion – Containment Procedures

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Network Intrusion (Containment Procedures)        |
| Document ID    | IR-PB-NI-005                                                 |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | SOC Manager / Network Security Lead / IR Team Lead           |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 network intrusion incident     |

---

## 2. Purpose

This document defines standardized containment procedures for network intrusion incidents affecting enterprise and MSSP-managed environments.

Network containment is one of the most sensitive phases of incident response because improper containment can:

- Alert the attacker and cause evidence destruction
- Disrupt critical business operations
- Break production connectivity
- Cause cascading outages across network segments
- Destroy volatile forensic artifacts

Containment must therefore be:

- Structured
- Approved when required
- Proportional to incident severity
- Documented
- Coordinated across SOC, Network, and IR Teams

The objective of containment is to:

- Stop active malicious activity
- Prevent further lateral movement
- Block command and control channels
- Prevent data exfiltration
- Preserve forensic evidence
- Reduce blast radius
- Stabilize environment for eradication

---

## 3. Scope

Applies to containment of:

- External perimeter intrusions
- Internal lateral movement
- Confirmed C2 communication
- VPN compromise
- Segmentation bypass
- Network-based data exfiltration
- Domain controller compromise
- Multi-segment network compromise
- MSSP client network intrusion cases

---

## 4. Containment Strategy Principles

### 4.1 Preserve Before Blocking

Where possible:

- Capture logs before blocking IPs
- Preserve NetFlow and DNS logs
- Initiate packet capture before firewall changes
- Acquire memory before host shutdown

Avoid:

- Immediate shutdown of compromised host (unless critical)
- Global firewall blocks without scope understanding
- Deleting attacker artifacts before analysis

---

### 4.2 Contain the Host Before the Network

Prefer:

- Isolating compromised endpoints first
- Blocking outbound traffic from specific host
- Limiting host network access to investigation subnet

Instead of:

- Blocking entire subnet immediately
- Disabling entire VLAN

---

### 4.3 Segment, Don’t Disconnect

When possible:

- Move host to quarantine VLAN
- Apply restrictive ACL
- Block high-risk ports
- Maintain forensic connectivity

Avoid:

- Immediate power-off
- Network disconnection without evidence capture

---

### 4.4 Coordinate Before High-Impact Changes

The following require approval from SOC Lead or IR Team:

- Disabling domain controllers
- Blocking large IP ranges
- Resetting all privileged credentials
- Disabling VPN access globally
- Shutting down network segments
- Removing firewall peering

---

## 5. Containment Workflow Overview

| Phase   | Goal                                   | Owner                  |
| -------- | -------------------------------------- | ---------------------- |
| Phase 1  | Confirm active threat presence         | L2 / L3                |
| Phase 2  | Identify containment scope             | L2 / SOC Lead          |
| Phase 3  | Select containment strategy            | SOC Lead / IR Team     |
| Phase 4  | Execute containment controls           | Network Team / IR      |
| Phase 5  | Validate containment effectiveness      | L2 / L3                |
| Phase 6  | Monitor for reinfection or pivoting    | SOC                    |

---

# 6. Containment Scenarios

---

## 6.1 Confirmed C2 Communication

### Objective:
Immediately stop attacker remote control.

### Actions:

| Step | Action | Owner | Approval |
|------|--------|--------|----------|
| 1 | Initiate packet capture | L2 | None |
| 2 | Block malicious IP/domain at firewall | Network Team | SOC Lead |
| 3 | Block domain at DNS resolver | Network Team | SOC Lead |
| 4 | Isolate compromised host | Network Team | SOC Lead |
| 5 | Preserve host memory | L3 | IR Lead |

### Validation:

- Confirm no further outbound connection attempts
- Monitor DNS for continued resolution attempts
- Review firewall deny logs

---

## 6.2 Compromised Endpoint

### Objective:
Prevent lateral movement and evidence destruction.

### Actions:

| Step | Action | Owner | Approval |
|------|--------|--------|----------|
| 1 | Move host to quarantine VLAN | Network Team | SOC Lead |
| 2 | Block outbound internet access | Network Team | SOC Lead |
| 3 | Preserve memory and disk | L3 | IR Lead |
| 4 | Disable compromised account | IAM Team | SOC Lead |

Avoid powering off until evidence is preserved.

---

## 6.3 Lateral Movement Detected

### Objective:
Prevent attacker expansion.

### Actions:

| Step | Action | Owner | Approval |
|------|--------|--------|----------|
| 1 | Identify all affected hosts | L2 | None |
| 2 | Isolate compromised systems | Network Team | SOC Lead |
| 3 | Block SMB/RDP between segments | Network Team | SOC Lead |
| 4 | Reset privileged credentials | IAM Team | SOC Lead |
| 5 | Increase logging on sensitive systems | Network Team | SOC Lead |

---

## 6.4 VPN Compromise

### Objective:
Stop unauthorized remote access.

### Actions:

| Step | Action | Owner | Approval |
|------|--------|--------|----------|
| 1 | Disable compromised VPN account | IAM Team | SOC Lead |
| 2 | Terminate active VPN sessions | Network Team | SOC Lead |
| 3 | Reset credentials and enforce MFA | IAM Team | SOC Lead |
| 4 | Review recent VPN login history | L2 | None |

---

## 6.5 Domain Controller Access Confirmed

### Objective:
Prevent enterprise-wide compromise.

### Actions:

| Step | Action | Owner | Approval |
|------|--------|--------|----------|
| 1 | Activate IR Team | SOC Lead | CISO |
| 2 | Isolate affected domain controller | Network Team | IR Lead |
| 3 | Preserve memory and disk | L3 | IR Lead |
| 4 | Reset all privileged credentials | IAM Team | CISO |
| 5 | Audit all domain admin accounts | L2 | IR Lead |

---

## 6.6 Data Exfiltration in Progress

### Objective:
Stop active data theft.

### Actions:

| Step | Action | Owner | Approval |
|------|--------|--------|----------|
| 1 | Block outbound traffic immediately | Network Team | IR Lead |
| 2 | Identify destination IP/domain | L2 | None |
| 3 | Preserve network logs | L2 | None |
| 4 | Activate Data Breach playbook | IR Team | CISO |
| 5 | Assess scope of transferred data | L3 | IR Lead |

---

## 6.7 Rogue Internal Device

### Objective:
Prevent unauthorized internal access.

### Actions:

| Step | Action | Owner | Approval |
|------|--------|--------|----------|
| 1 | Disable switch port | Network Team | SOC Lead |
| 2 | Identify device MAC address | Network Team | None |
| 3 | Review DHCP logs | L2 | None |
| 4 | Investigate asset ownership | IT Team | SOC Lead |

---

## 6.8 DNS Tunneling or Protocol Abuse

### Objective:
Disrupt covert communication channel.

### Actions:

| Step | Action | Owner | Approval |
|------|--------|--------|----------|
| 1 | Block malicious domain | Network Team | SOC Lead |
| 2 | Implement DNS sinkhole | Network Team | SOC Lead |
| 3 | Capture DNS traffic | L3 | IR Lead |
| 4 | Isolate affected host | Network Team | SOC Lead |

---

# 7. Containment Control Matrix

| Threat Type | Primary Control | Secondary Control |
|-------------|----------------|------------------|
| C2 | Firewall block | DNS block |
| Lateral Movement | ACL segmentation | Credential reset |
| VPN compromise | Disable account | Enforce MFA |
| Data exfiltration | Egress block | DLP enforcement |
| Domain admin abuse | Reset privileged accounts | Increase monitoring |
| Malware host | Host isolation | EDR containment |
| SMB abuse | Disable SMB between segments | Network segmentation |

---

# 8. High-Risk Containment Actions

The following actions require IR Lead or CISO approval:

| Action | Risk |
|--------|------|
| Disabling entire VLAN | Business outage |
| Resetting all domain accounts | Operational disruption |
| Blocking entire country IP range | Collateral service disruption |
| Disabling VPN globally | Workforce impact |
| Shutting down production server | Revenue impact |

---

# 9. Containment Validation

After containment actions are executed:

- Confirm malicious IPs are blocked
- Verify no further C2 communication
- Confirm no further lateral movement attempts
- Monitor logs for reattempted connections
- Validate account resets took effect
- Ensure monitoring rules remain active
- Confirm attacker persistence mechanisms removed

---

## 9.1 Validation Checklist

| Validation Item | Status |
|-----------------|--------|
| Malicious IP blocked | ☐ |
| DNS block applied | ☐ |
| Compromised hosts isolated | ☐ |
| Privileged credentials reset | ☐ |
| Lateral movement stopped | ☐ |
| Exfiltration stopped | ☐ |
| Logging preserved | ☐ |
| Monitoring enhanced | ☐ |

---

# 10. Communication Requirements

For P1/P2 incidents:

- Notify SOC Lead immediately
- Update management per escalation matrix
- Initiate bridge call if required
- Provide status updates every 30 minutes
- Notify Legal if data exposure suspected

Reference:
`05_ESCALATION-AND-COMMUNICATION/`

---

# 11. MSSP Considerations

For MSSP-managed environments:

- Confirm tenant isolation
- Prevent cross-client impact
- Notify client per SLA
- Obtain client approval for major containment actions
- Document all containment actions in client ticket
- Ensure shared infrastructure not impacted

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

# 12. Transition to Eradication

Containment is not resolution.

After containment:

- Begin eradication phase
- Remove persistence mechanisms
- Patch exploited vulnerabilities
- Harden segmentation
- Update firewall rules permanently
- Conduct credential hygiene review
- Update detections

Reference:
`02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L3-Forensics.md`

---

## 13. Related Documents

| Document | Path |
|----------|------|
| Network Intrusion Master | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md` |
| Network Intrusion L2 | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L2-Investigation.md` |
| Network Intrusion L3 | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L3-Forensics.md` |
| Network Intrusion MITRE Mapping | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-MITRE-Mapping.md` |
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| Data Breach Playbook | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 14. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | SOC Manager / Network Security Lead | Initial version |

---

## 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**