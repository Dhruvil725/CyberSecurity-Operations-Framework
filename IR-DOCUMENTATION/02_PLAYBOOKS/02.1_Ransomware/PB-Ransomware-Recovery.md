# Playbook: Ransomware – Recovery

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Ransomware (Recovery) |
| Document ID | IR-PB-RAN-007 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | IT Operations Manager / IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 ransomware incident |

---

## 2. Purpose

This document defines the recovery procedures for ransomware incidents.
Recovery is the controlled restoration of systems, data, and services to a
known-good state after containment and eradication.

Recovery must ensure:
- restoration does not reintroduce attacker persistence or malware
- business services are restored in priority order
- integrity and security validation occurs before return-to-service
- post-recovery monitoring detects re-entry or residual activity
- all recovery actions are documented and approved

---

## 3. Scope

Applies to:
- endpoints and servers impacted by ransomware
- file shares and storage systems
- critical infrastructure (identity systems, backup systems)
- cloud resources and SaaS services (where impacted)
- enterprise and MSSP client environments

Includes:
- restoration from backups
- rebuild and reconfiguration
- data validation and integrity checks
- controlled reintroduction to network and production services

---

## 4. Preconditions (Must Be True Before Recovery)

Recovery begins only when all conditions are met:

1. containment verified (no active encryption or spread)
2. eradication completed (persistence removed; access paths closed)
3. compromised accounts remediated (password reset + session revocation)
4. backups verified as clean (no evidence of tampering/encryption)
5. entry vector remediation completed (patch/workaround applied)
6. IR Team approval for recovery start

References:
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md`
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md`

---

## 5. Recovery Objectives and Outputs

### 5.1 Objectives
- restore critical services and data safely
- minimize downtime and business disruption
- validate system integrity and operational functionality
- ensure no attacker persistence remains
- implement enhanced monitoring during recovery window
- capture documentation for final report and audit readiness

### 5.2 Outputs (Minimum)
- recovery plan with priority order and owners
- restore/rebuild action log (what/when/who)
- return-to-service approvals recorded
- integrity validation evidence
- post-recovery monitoring plan and results
- incident closure readiness confirmation

---

## 6. Recovery Planning (Required)

### 6.1 Service Restoration Priority

Prioritize restoration based on business impact. Example categories:

| Priority | Service Type | Examples |
|---------|--------------|----------|
| 1 | Identity and Core Access | AD, SSO, DNS, DHCP, MFA, PKI |
| 2 | Backup and Recovery Systems | backup servers, repositories, DR systems |
| 3 | Core Business Applications | ERP, finance, payment systems, customer portals |
| 4 | File Services and Collaboration | file servers, SharePoint, document management |
| 5 | End-User Devices | user endpoints, VDI, laptops |
| 6 | Non-Critical Systems | dev/test, low-critical apps |

The final order must be confirmed by business owners and IT leadership.

### 6.2 Recovery Method Selection

| Method | When Used | Notes |
|-------|-----------|------|
| Restore from backup | data encrypted but backups intact | ensure clean backup validation |
| Rebuild from golden image | integrity uncertain or critical servers | recommended for high-value assets |
| Snapshot restore (virtualization/cloud) | controlled environments with trustworthy snapshots | validate snapshot timestamp and integrity |
| Decrypt using verified decryptor | only when trusted decryptor exists | do not rely on attacker tools |
| Manual data reconstruction | limited scope or critical data not in backups | requires strong validation |

---

## 7. Backup Validation (Critical Requirement)

Before restoring:
- identify last known good backup timestamp for each system
- confirm backup repository was not accessible by attacker
- confirm backups are not encrypted or altered
- perform test restore in isolated environment where feasible
- scan restored data using EDR/AV before production use

Backup validation evidence must be recorded in the ticket.

---

## 8. Recovery Execution Workflow

### Phase 1: Build Clean Recovery Environment

Actions:
- ensure recovery network segment is clean and isolated
- restrict admin access to recovery environment
- ensure EDR agents and logging are active on rebuilt systems
- ensure time synchronization and logging policies are correct
- implement temporary restrictive firewall rules for recovery segment

Outputs:
- recovery environment readiness confirmation
- access control list for recovery actions

---

### Phase 2: Restore/Rebuild Systems (Controlled Order)

For each system, perform:

1. rebuild or restore to known-good state
2. apply patches and configuration baseline
3. install security tooling (EDR, logging agents)
4. validate system integrity and functionality in isolation
5. reconnect to network under monitoring

Required documentation per system:
- restore/rebuild method used
- backup timestamp or build version
- validation results (scan and functional tests)
- reconnection approval and time

---

### Phase 3: Data Restoration and Integrity Verification

For restored data:
- scan data for malware indicators
- check for suspicious file extensions or ransom artifacts
- validate data completeness and correctness with data owners
- confirm permissions and access controls are correct
- confirm no public exposures exist in cloud storage (if applicable)

---

### Phase 4: Return-to-Service (RTS) and Monitoring

RTS should occur only after:
- security validation passed
- business owner confirms function is acceptable
- IR Team confirms risk is acceptable for production

Post-RTS monitoring must be enabled for the defined window.

---

## 9. Recovery Validation Checklists

### 9.1 System Integrity Checklist (Minimum)
- EDR agent installed and healthy
- no active detections in EDR
- no suspicious scheduled tasks/services/autoruns
- OS and application patches applied
- correct baseline configuration applied
- correct local admin accounts present (no unknown accounts)
- logs being generated and forwarded to SIEM
- outbound connections verified (no suspicious destinations)

### 9.2 Business Functionality Checklist
- application starts successfully
- user authentication works
- expected transactions/operations complete
- performance acceptable
- error rates normal
- dependent services reachable

### 9.3 Access Control Checklist
- privileged access restricted
- MFA enforced where applicable
- shared admin credentials rotated
- least privilege restored
- service account usage validated

---

## 10. Return-to-Service Approval (Mandatory for P1/P2)

RTS approval must be recorded in the incident ticket.

Recommended approvers:

| System Criticality | Minimum Approval |
|-------------------|------------------|
| Business-critical service | Business Owner + IT Ops Lead + IR Team Lead + SOC Lead |
| Identity infrastructure | IAM Lead + IR Team Lead + CISO (for P1) |
| Backup platform | Backup Owner + IR Team Lead |
| Non-critical systems | IT Ops Lead + SOC Lead |

Record:
- approver name and role
- timestamp
- system name
- risk acceptance statement (if any)

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md`

---

## 11. Post-Recovery Monitoring (Required)

### 11.1 Monitoring Window Recommendations
| Severity | Minimum Monitoring Window |
|---------|----------------------------|
| P1 | 72 hours enhanced monitoring |
| P2 | 48 hours enhanced monitoring |
| P3 | 24 hours enhanced monitoring |

### 11.2 Monitoring Activities
- EDR watchlists for the IOC set discovered during incident
- SIEM correlation rules for:
  - suspicious remote execution tools
  - credential dumping indicators
  - new admin account creation
  - new scheduled task/service creation
  - outbound connections to suspicious destinations
- identity monitoring:
  - new MFA device enrollment
  - admin group membership changes
  - unusual sign-in patterns
- backup monitoring:
  - repository access
  - deletion/tampering alerts

### 11.3 Monitoring Output
- daily monitoring summary in ticket or daily SOC report
- any re-entry indicator must trigger immediate re-escalation

---

## 12. Recovery Risks and Controls

| Risk | Impact | Control |
|------|--------|---------|
| restoring infected backups | reinfection | backup validation and test restores |
| reintroducing compromised credentials | attacker returns | credential reset + session revoke |
| reconnecting systems too early | renewed spread | RTS gate controls and approvals |
| missing persistence | attacker persists | forensic verification and hunting |
| incomplete logging after rebuild | reduced visibility | validate log forwarding and SIEM ingestion |
| business pressure to restore quickly | risk acceptance issues | document approval and risk decisions |

---

## 13. Recovery Documentation Requirements

Minimum documents/evidence for the incident package:
- system restore list with timestamps
- backup validation results
- RTS approvals and sign-offs
- post-recovery monitoring results
- changes implemented (patches, firewall rules, IAM changes)
- lessons learned inputs related to recovery

These are required for audit and compliance evidence.

Reference:
`07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`

---

## 14. MSSP Client Recovery Notes

For MSSP clients:
- confirm which recovery activities are MSSP responsibility vs client responsibility
- document client approvals and coordination steps
- ensure evidence and documentation remain client-scoped
- provide recovery guidance in client-facing incident report
- ensure client SLA reporting includes recovery milestones

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`

---

## 15. Related Documents

| Document | Path |
|---------|------|
| Ransomware Master | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md` |
| Containment | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md` |
| L3 Forensics | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md` |
| Incident Closure Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| PIR Template | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md` |

---

## 16. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | IT Ops Manager / IR Team Lead | Initial version |

---

## 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document