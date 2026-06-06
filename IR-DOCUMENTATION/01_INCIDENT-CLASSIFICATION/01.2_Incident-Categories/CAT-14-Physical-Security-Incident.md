# CAT-14 – Physical Security Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Physical Security Incident |
| Document ID | IR-CAT-014 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Category Overview

| Field | Details |
|-------|---------|
| Category ID | CAT-14 |
| Default Severity | P2 – High (confirmed theft/tampering of critical assets) / P3 – Medium (suspicious physical activity) / P1 – Critical (data center compromise or impact to critical services) |
| Escalation Priority | High due to potential impact on confidentiality, availability, and safety |
| Attack Goal | Theft, sabotage, unauthorized access, device compromise, disruption |
| Threat Actors | External intruders, insiders, contractors, opportunistic thieves |
| Coordination | Facilities, Security Guards, IT Operations, HR, Legal, SOC |
| Playbook Reference | `02_PLAYBOOKS/` (category-driven; physical incident procedures are cross-functional) |

---

## 3. What is a Physical Security Incident?

A physical security incident is any event involving unauthorized access,
theft, damage, or tampering with physical facilities, systems, or assets
that may affect information security.

Physical security incidents can lead to:

- Theft of endpoints or removable media containing sensitive data
- Unauthorized access to server rooms, network closets, or work areas
- Hardware tampering leading to malware implantation or credential theft
- Disruption of business operations due to sabotage or damage
- Regulatory and contractual reporting obligations (depending on impact)

Physical incidents often require immediate coordination with facilities,
security personnel, and law enforcement where applicable.

---

## 4. Common Physical Security Scenarios

| Scenario | Description |
|---------|-------------|
| Lost or Stolen Laptop | Device with corporate access lost or stolen |
| Lost Phone/Tablet | Mobile device with email/SSO access lost |
| Unauthorized Data Center Access | Unauthorized entry into controlled facility |
| Theft of Removable Media | USB drives, backup tapes, external disks stolen |
| Tailgating | Unauthorized person follows employee into secure area |
| Hardware Tampering | Keyloggers, rogue devices, modified workstations |
| Rogue Network Device | Unauthorized switch/AP inserted into network |
| Badge Abuse | Stolen badge, cloned badge, access misuse |
| CCTV Failure | CCTV tampered, disabled, or unavailable during incident |
| Physical Damage/Sabotage | Intentional damage to network, power, or equipment |
| Secure Document Theft | Theft of printed sensitive documents |

---

## 5. Indicators and Observables

### 5.1 Facility and Access Observables

| Indicator | Details |
|----------|---------|
| Badge Access Anomalies | Access outside business hours or unusual locations |
| Multiple Failed Badge Attempts | Repeated denied badge entries |
| Tailgating Reports | Employees observe unauthorized entry |
| Door Forced Open | Physical signs of forced entry |
| CCTV Alerts | Camera offline, coverage gaps, tampering indicators |
| Unapproved Visitor | Visitor without escort or unauthorized access attempt |

### 5.2 Asset and Device Observables

| Indicator | Details |
|----------|---------|
| Missing Device | Laptop/phone/server hardware missing |
| Tamper Evidence | Broken seals, opened chassis, unknown devices attached |
| Rogue Peripheral | Unknown USB device, hardware keylogger, malicious cable |
| Rogue Network Gear | Unknown AP, switch, or network tap in closet |
| Unexpected BIOS/UEFI Changes | Boot order changes or firmware alterations |
| Disk Removal | Storage devices removed from servers or workstations |

### 5.3 Log Sources to Review

| Source | What to Review |
|--------|----------------|
| Badge Access Logs | Time, door, user, deny/allow events |
| Visitor Logs | Visitor identity, escort, sign-in/sign-out |
| CCTV Footage | Relevant time window and camera angles |
| Asset Inventory | Device assignment records and serial numbers |
| EDR/MDM Logs | Last check-in, device location, device state |
| Network Logs | New MAC addresses, rogue AP detection, switch port changes |
| IT Change Records | Authorized maintenance that may explain physical presence |

---

## 6. Severity Classification

| Scenario | Severity |
|----------|----------|
| Unauthorized access to data center with potential system tampering | P1 – Critical |
| Physical sabotage causing outage of critical services | P1 – Critical |
| Theft of server hardware, backup media, or sensitive storage | P1 – Critical |
| Confirmed theft of laptop with sensitive data and no encryption | P1 – Critical |
| Confirmed theft/loss of corporate endpoint (encrypted) | P2 – High |
| Confirmed insertion of rogue network device in secure area | P2 – High |
| Physical tampering suspected on workstation/server | P2 – High |
| Tailgating or suspicious access attempt (no confirmed access) | P3 – Medium |
| Minor facility incident with no information security impact | P4 – Low |

---

## 7. Immediate Response Actions

### 7.1 First 15 Minutes

- Create incident ticket and assign initial severity
- Notify SOC Lead for P2 and above
- Notify physical security / facilities immediately for all physical incidents
- Preserve evidence:
  - badge access logs (export immediately)
  - CCTV footage (secure relevant time window)
  - visitor logs (capture details)
- Identify affected assets:
  - device type, owner, asset tag, serial number
  - last known location and time
- If device is stolen/lost and managed by MDM/EDR:
  - trigger lock/wipe actions as per policy and approval
  - disable device account access where applicable (conditional access, certificates)

### 7.2 First 1 Hour

- Determine whether sensitive data exposure is likely:
  - encryption status (disk encryption enabled/verified)
  - offline access possibility
  - stored credentials or tokens present
- Disable/revoke access:
  - disable user sessions and tokens (if device compromise risk)
  - rotate VPN certificates or device-bound credentials if used
- Coordinate with HR and Legal if employee involvement suspected
- Engage law enforcement if theft or break-in is confirmed (as required)
- For network device insertion:
  - isolate switch port or network segment
  - identify connected devices and MAC addresses
  - preserve device as evidence (do not power off if volatile evidence needed)

### 7.3 First 4 Hours

- For suspected tampering:
  - remove device from production use
  - preserve as evidence under chain-of-custody
  - perform forensic examination (disk/memory, firmware checks) as required
- For lost endpoints:
  - confirm wipe/lock status from MDM/EDR
  - document confirmation evidence
- Scope access logs:
  - verify who accessed the location and when
  - correlate with CCTV and visitor records
- Provide management update for P1/P2 incidents
- Notify clients if MSSP-managed client assets or facilities are involved

---

## 8. Containment and Recovery Guidance

| Action | Use When | Notes |
|-------|----------|------|
| Remote Wipe / Lock | Lost or stolen managed devices | Confirm wipe/lock completion and record evidence |
| Disable Device Certificates | Device-bound VPN/cert access | Coordinate with IAM/PKI teams |
| Session Revocation | Device may contain active tokens | Pair with password reset if needed |
| Network Port Shutdown | Rogue device detected | Preserve evidence and capture configuration first |
| Replace Hardware | Tampering or theft confirmed | Ensure secure disposal of compromised components |
| Forensic Imaging | Suspicious tampering | Maintain chain-of-custody for legal defensibility |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 9. Investigation Questions

1. What asset or facility was impacted and what is its criticality?
2. Is the incident theft, loss, unauthorized access, or tampering?
3. What evidence exists (badge logs, CCTV, witness statements)?
4. Who had authorized access to the area during the time window?
5. Was the device encrypted and centrally managed (EDR/MDM status)?
6. Does the device have cached credentials, VPN profiles, or access tokens?
7. Was the device last online, and can it be located or locked remotely?
8. Was any rogue device inserted into the network (MAC address, switch port, AP SSID)?
9. Is there any indication of data exposure (DLP logs, unusual access events)?
10. Does this require HR/Legal/law enforcement involvement?
11. Is client data or regulated data potentially affected?
12. What additional controls must be implemented to prevent recurrence?

---

## 10. Critical Do's and Do Not's

### Do

- Preserve badge logs and CCTV evidence immediately (they may be overwritten)
- Treat physical evidence carefully and maintain chain-of-custody
- Confirm encryption and MDM/EDR status for lost/stolen devices
- Revoke tokens and access if device compromise is plausible
- Coordinate with facilities, HR, and legal early for serious incidents
- Document every action taken and approvals received

### Do Not

- Handle or modify suspected tampered devices without evidence preservation
- Delay CCTV preservation (many systems overwrite footage quickly)
- Assume device encryption without verified proof
- Publicly share incident details without management/legal approval
- Return suspected tampered equipment to production

---

## 11. Escalation Path

| Stage | Action |
|-------|--------|
| Reporter / Facilities | Report incident to SOC and physical security |
| L1 Triage | Open ticket, preserve initial evidence, notify SOC Lead if needed |
| SOC Lead | Coordinate response and communications for P2/P1 incidents |
| Facilities / Physical Security | Secure location, collect CCTV and access logs |
| IT Operations | Disable access, lock/wipe device, isolate network segments |
| IR Team | Evidence handling and forensic support where required |
| HR / Legal | Employee involvement, disciplinary/legal process guidance |
| Management / CISO | Major incident oversight and disclosure decisions |
| MSSP SDM / Client Owner | Client notification and coordination where applicable |

---

## 12. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Device contains sensitive/regulatory data and may be exposed | Engage Compliance and Legal |
| Data center compromise with service impact | Treat as major incident and assess reporting |
| MSSP client asset/facility impacted | Notify client per SLA and contract |
| Theft confirmed | Consider law enforcement engagement and insurance requirements |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 13. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| Badge access logs export | Critical | Include deny/allow events and door IDs |
| CCTV footage export | Critical | Preserve full time window; ensure integrity |
| Visitor logs | High | Visitor identity and escort details |
| Asset inventory records | High | Asset tag, serial, user assignment |
| MDM/EDR status reports | High | Last check-in, wipe/lock confirmation |
| Network switch logs | High | MAC address, port changes, rogue devices |
| Photographs | Medium | Scene photos, tamper evidence, device state |
| Witness statements | Medium | Document who observed what and when |
| Chain-of-custody forms | As needed | Required if evidence may be used legally |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Insider Threat Category | `01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-05-Insider-Threat.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| Contact Directory | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| Policy Exception Register | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**