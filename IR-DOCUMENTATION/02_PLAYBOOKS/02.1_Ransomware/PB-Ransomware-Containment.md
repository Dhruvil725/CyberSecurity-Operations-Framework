# Playbook: Ransomware – Containment

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Ransomware (Containment) |
| Document ID | IR-PB-RAN-005 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 ransomware incident |

---

## 2. Purpose

This document defines the containment procedures for ransomware incidents.
It provides structured, prioritized actions to stop the spread of ransomware,
protect critical assets, and preserve business continuity while maintaining
evidence integrity.

Containment is the critical bridge between detection and eradication.
Improper containment can lead to:
- continued encryption and data loss
- lateral movement to additional systems
- destruction of backups and recovery options
- reinfection during recovery

---

## 3. Scope

Applies to:
- active ransomware encryption incidents
- ransomware precursor incidents with confirmed lateral movement
- enterprise and MSSP client environments
- on-premises, cloud, and hybrid infrastructure

Includes:
- endpoint and server isolation
- network segmentation
- identity and access control
- backup protection
- communication and approval workflows

---

## 4. Containment Principles

1. **Speed over Perfection**: Act quickly to stop spread; refinement comes later
2. **Preserve Evidence**: Do not destroy artifacts needed for investigation
3. **Protect Critical Assets**: Prioritize domain controllers, backups, and critical servers
4. **Maintain Chain of Command**: Follow approval matrix for high-impact actions
5. **Document Everything**: Every containment action must be timestamped and logged
6. **Assume Persistence**: Contain as if attacker has multiple access paths

---

## 5. Containment Priority Order (Non-Negotiable Sequence)

| Priority | Objective | Actions |
|----------|-----------|---------|
| P0 | Stop Active Encryption | Isolate actively encrypting hosts immediately |
| P1 | Protect Identity Systems | Secure AD, privileged accounts, SSO |
| P2 | Protect Backups | Isolate backup infrastructure; prevent deletion |
| P3 | Stop Lateral Movement | Segment network; block admin protocols |
| P4 | Stop Exfiltration | Block C2/exfil destinations |
| P5 | Prevent Reinfection | Reset credentials; patch entry vector |

---

## 6. Detailed Containment Procedures

### Phase 1: Immediate Isolation (First 15 Minutes)

#### 6.1 Isolate Actively Encrypting Hosts

**Detection Methods**:

- EDR showing mass file modification
- User reports of files becoming inaccessible
- High disk I/O with suspicious process

**Isolation Methods** (in order of preference):

| Method | When to Use | Approval Required |
|--------|-------------|-------------------|
| EDR Network Containment | Endpoint has EDR agent | L2/SOC Lead (emergency) |
| Switch Port Shutdown | Server/network device; no EDR | SOC Lead + Network Team |
| VLAN Segmentation | Multiple hosts in same segment | SOC Lead + Network Team |
| Physical Disconnection | Critical server; other methods fail | SOC Lead + IT Ops |

**Documentation Required**:
- Hostname and IP
- Time of isolation
- Method used
- Business impact assessment
- Approver name and time

#### 6.2 Emergency Account Actions

Immediately disable or revoke:
- compromised user accounts (confirmed or high confidence)
- service accounts showing suspicious activity
- privileged accounts if compromise suspected

**Session Revocation**:
- Azure AD / Entra ID: revoke sessions immediately
- AD: logoff forced via script or wait for ticket expiration (if Kerberos)
- VPN: kill active sessions
- Cloud admin portals: revoke tokens

**Password Resets**:
- reset passwords for compromised accounts
- force password change at next logon for suspected accounts
- prioritize privileged accounts

---

### Phase 2: Protect Critical Infrastructure (15–60 Minutes)

#### 6.3 Domain Controller and AD Protection

Actions:
- enable enhanced logging on all DCs immediately
- monitor for DCSync, DCShadow, or unusual replication
- check for new admin group memberships
- disable NTLM if not required (emergency hardening)
- restrict RDP to DCs to specific admin jump hosts only

If DC compromise is suspected:
- isolate affected DC (replication pause)
- seize FSMO roles if necessary
- prepare for DC rebuild or forest recovery (worst case)

#### 6.4 Backup Infrastructure Protection

Critical actions:
- immediately disconnect backup repositories from network (logical isolation)
- verify backup admin accounts are not compromised
- check backup job logs for deletion or tampering
- enable immutable backup features if available
- document last known good backup timestamps

**Never allow backup systems to remain accessible from infected segments.**

---

### Phase 3: Network Containment (30–120 Minutes)

#### 6.5 Network Segmentation

Implement emergency segmentation:

| Segment Action | Purpose | Implementation |
|---------------|---------|----------------|
| Isolate infected VLAN | Stop east-west spread | Firewall rule or ACL |
| Block SMB/RDP between segments | Stop lateral movement | Firewall deny rules |
| Restrict internet from server segments | Stop C2/exfil | Default deny outbound |
| Create quarantine VLAN | Isolate suspicious hosts | Move hosts to isolated VLAN |

#### 6.6 IOC Blocking

Block at multiple layers simultaneously:

**DNS Layer**:
- block ransomware C2 domains
- block exfiltration destinations
- implement DNS sinkhole for known bad domains

**Proxy/Firewall Layer**:
- block IP addresses and ranges
- block suspicious user-agents
- block unusual ports (if not business-required)

**EDR Layer**:
- block known file hashes
- block suspicious parent-child process chains
- enable aggressive behavioral blocking

---

### Phase 4: Identity and Access Lockdown (60–180 Minutes)

#### 6.7 Privileged Access Emergency Controls

- disable privileged accounts not required for incident response
- implement emergency break-glass admin accounts (new, uncompromised)
- enforce MFA on all remaining admin accounts
- restrict admin logins to specific hardened jump hosts
- monitor all privileged activity in real-time

#### 6.8 Remote Access Hardening

- disable VPN access for compromised accounts
- restrict VPN to specific IP allow-lists (emergency)
- disable external RDP entirely if not already blocked
- review and revoke OAuth consents for suspicious applications

---

## 7. Containment Action Approval Matrix

| Action | L2 Approval | SOC Lead Approval | Management Approval | IT Ops Execution |
|--------|-------------|-------------------|---------------------|------------------|
| EDR network contain (single endpoint) | Yes | Notify | - | - |
| Server isolation (production) | Recommend | Yes | If business-critical | Yes |
| Disable user account | Yes | If privileged | - | IAM/AD Team |
| Disable privileged account | Recommend | Yes | Domain Admin: Yes | IAM/AD Team |
| Network segmentation change | Recommend | Yes | Major segment: Yes | Network Team |
| Backup repository isolation | - | Yes | Yes | Backup/Storage Team |
| DC isolation | - | Yes | Yes (CISO) | IT Ops |
| Mass account disable (>10) | - | Yes | Yes | IAM/AD Team |
| Emergency firewall changes | - | Yes | Yes | Network Team |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 8. Verification of Containment Effectiveness

After containment actions, verify:

### 8.1 Encryption Stopped Verification
- monitor EDR for continued file modification on isolated hosts
- check file share logs for ongoing rename/encryption activity
- confirm no new ransom notes appearing

### 8.2 Lateral Movement Stopped Verification
- monitor for new SMB/RDP connections from isolated segments
- check authentication logs for new suspicious sign-ins
- monitor for new host discoveries or scanning

### 8.3 C2 Communication Stopped Verification
- monitor proxy/firewall logs for continued beaconing attempts
- check DNS query logs for blocked domain attempts
- confirm no new outbound connections to attacker infrastructure

### 8.4 Backup Protection Verification
- confirm backup repositories are inaccessible from infected segments
- verify backup jobs can still run (if safely configured)
- check backup integrity (spot-check restore capability)

---

## 9. Communication During Containment

### 9.1 Internal Communication
- SOC Lead provides containment status updates per SLA
- IT Ops confirms execution of technical changes
- Management informed of business impact and timeline

### 9.2 Client Communication (MSSP)
- inform client of containment actions taken
- request approval for pending high-impact actions
- confirm client understanding of business impact

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

## 10. Common Containment Mistakes to Avoid

| Mistake | Impact | Prevention |
|--------|--------|------------|
| Isolating only one host while missing lateral spread | continued encryption | always check for lateral movement before declaring containment complete |
| Failing to protect backups first | permanent data loss | isolate backup infrastructure as P1 priority |
| Disabling accounts without revoking sessions | attacker remains active | always revoke sessions and tokens |
| Blocking too broadly (entire regions) | business disruption | use surgical blocks based on confirmed IOCs |
| Not documenting containment actions | audit/regulatory failure | timestamp and document every action in ticket |
| Assuming containment is permanent | reinfection | monitor for new connections and persistence |

---

## 11. Transition to Eradication

Containment is complete when:
- active encryption is stopped on all known systems
- no new systems are showing encryption behavior
- lateral movement pathways are blocked
- critical assets (AD, backups) are protected
- C2 communications are blocked

**Do not proceed to eradication until containment is verified.**

Reference:
`02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md`

---

## 12. Related Documents

| Document | Path |
|---------|------|
| Ransomware Master | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md` |
| L1 Triage | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L1-Triage.md` |
| L2 Investigation | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L2-Investigation.md` |
| L3 Forensics | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md` |
| Eradication | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md` |
| Recovery | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md` |
| Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Network Isolation SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Isolation-Procedure.md` |

---

## 13. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

## 14. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document