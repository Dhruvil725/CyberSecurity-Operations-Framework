# Playbook: Ransomware – Eradication

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Ransomware (Eradication) |
| Document ID | IR-PB-RAN-006 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 ransomware incident |

---

## 2. Purpose

This document defines the eradication procedures for ransomware incidents.
Eradication is the phase in which the attacker’s access, malware, tools,
and persistence mechanisms are removed from the environment, and the
original entry vector is closed to prevent reinfection.

Eradication must occur only after containment has been verified.

---

## 3. Scope

Applies to:
- all confirmed compromised hosts (endpoints, servers, cloud workloads)
- identities and access paths used by attacker
- persistence mechanisms and tooling
- exploited vulnerabilities and misconfigurations
- ransomware precursor toolchains and post-exploitation frameworks

Includes:
- host cleanup or rebuild decisions
- credential and secret rotation
- configuration hardening
- validation steps to confirm eradication success

---

## 4. Preconditions (Must Be True Before Eradication)

Eradication begins only when containment conditions are met:

- active encryption is stopped
- no new systems are being encrypted
- lateral movement is blocked or controlled
- compromised accounts are identified (at least initial set)
- backups and critical infrastructure are protected
- evidence required for investigation has been preserved

Reference:
`02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md`

---

## 5. Eradication Objectives and Outputs

### 5.1 Objectives
1. Remove ransomware payload(s) and associated tooling
2. Remove persistence (host-based, identity-based, cloud-based)
3. Eliminate attacker access and re-entry paths
4. Patch exploited vulnerabilities and close exposed services
5. Rotate compromised credentials, secrets, and tokens
6. Validate environment is clean enough to begin recovery

### 5.2 Outputs (Minimum)
- eradication action log (what/when/who)
- confirmed list of persistence removed
- credential rotation record (accounts reset, tokens revoked)
- vulnerability remediation record (patches applied, exposure closed)
- final IOC block list applied (EDR/DNS/proxy/firewall)
- validation results proving eradication success
- updated scope list (confirmed cleaned vs pending)

---

## 6. Eradication Strategy (Decision Guidance)

### 6.1 Rebuild vs Clean
For high-risk ransomware incidents, rebuild is often safer than cleaning.

| Approach | When to Use | Advantages | Risks |
|:-------:|:-----------:|:---------:|:----:|
| Rebuild (recommended for servers and critical hosts) | DC compromise suspected, persistent access unclear, high integrity requirement | highest confidence clean state | longer recovery time |
| Clean (targeted removal) | single endpoint, clear artifact visibility, integrity verifiable | faster | risk of missed persistence |
| Hybrid | mix of rebuild + cleaning | balanced | requires tight coordination |

Decision must consider:
- business criticality
- evidence of persistence
- attacker dwell time
- available backups and golden images
- impact of downtime

---

## 7. Eradication Workstreams

Eradication is executed in parallel workstreams under Incident Commander control:

1. Host eradication (endpoints/servers)
2. Identity eradication (AD/SSO/MFA)
3. Network eradication (C2 blocks, segmentation persistence)
4. Cloud/SaaS eradication (tokens, OAuth, storage exposure)
5. Vulnerability remediation (entry vector closure)
6. Detection improvements (temporary rules during eradication)

---

## 8. Host Eradication Procedures

### 8.1 Host Triage Categories
Classify hosts into:

| Category | Meaning | Action |
|---------|---------|--------|
| Confirmed Compromised | ransomware/persistence confirmed | rebuild or clean immediately |
| Suspected Compromised | suspicious activity, same user/subnet | quarantine and investigate |
| Exposed but Clean | vulnerable but no evidence | patch/harden and monitor |
| Critical Control Plane | DC, backup, hypervisor | treat as highest priority rebuild if compromise suspected |

### 8.2 Standard Host Eradication Steps (Clean Option)
Perform only after evidence capture:

- remove malicious binaries and scripts
- remove persistence:
  - scheduled tasks
  - services
  - autoruns/run keys
  - startup items
  - WMI subscriptions (if used)
- remove attacker tools:
  - remote execution utilities
  - credential dumping tools
  - archived staging directories
- validate EDR sensor integrity and re-enable protections
- perform full EDR scan and verify no detections remain
- verify network connections no longer occur to suspicious destinations
- document all actions and artifacts removed

### 8.3 Standard Host Rebuild Steps (Preferred for Critical Hosts)
- preserve disk triage image (where required)
- rebuild system from known-good image
- patch to current baseline
- restore configuration from trusted baseline
- rejoin domain using verified clean credentials
- reinstall EDR and validate healthy status
- perform post-build validation and monitoring before reconnecting to production

---

## 9. Identity Eradication Procedures (Critical)

Identity compromise is the most common re-entry vector.

### 9.1 Account Remediation Categories
| Category | Examples | Action |
|---------|----------|--------|
| Privileged Admin Accounts | Domain Admin, Cloud Admin | immediate reset; session revoke; review group membership |
| Service Accounts | backup service, app service | reset with coordinated downtime plan |
| Standard Users | affected employees | reset; MFA check; session revoke |
| Vendor Accounts | third-party support | disable temporarily; re-enable with controls |

### 9.2 Required Identity Actions
- reset all confirmed compromised accounts
- revoke sessions and refresh tokens (cloud and SaaS)
- review and revert unauthorized group membership changes
- remove unauthorized accounts created by attacker
- enforce MFA for privileged identities (where possible)
- remove suspicious MFA devices and recovery methods
- audit and remove mailbox forwarding rules (if email account compromise)
- disable legacy authentication where possible during incident window
- document account changes with timestamps and approvers

### 9.3 “Credential Reset Order” Guidance
Recommended sequence:
1. privileged accounts used during intrusion
2. accounts with evidence of credential dumping exposure
3. service accounts with broad access
4. standard users in affected scope
5. break-glass accounts (validate separately)

---

## 10. Network and Perimeter Eradication

### 10.1 Block and Remove Attacker Infrastructure
- confirm all IOC blocks are deployed:
  - DNS block/sinkhole
  - proxy blocks
  - firewall blocks
  - EDR hash blocks
- verify blocks are effective through monitoring

### 10.2 Remove Lateral Movement Pathways
- restrict SMB/RDP between segments
- restrict admin access to jump hosts only
- disable unused remote admin services
- enforce network ACLs for server-to-server traffic
- review VPN posture and apply conditional access where possible

### 10.3 Validate No Residual C2
- monitor outbound traffic for beaconing patterns
- monitor DNS requests to newly registered domains
- validate EDR telemetry shows no suspicious external connections

---

## 11. Cloud and SaaS Eradication (If Applicable)

### 11.1 Token and Key Rotation
- rotate exposed access keys, API keys, and secrets
- revoke OAuth grants and remove malicious applications
- revoke sessions for compromised cloud identities

### 11.2 Configuration Hardening
- restore logging configurations and retention
- remove public access from storage
- apply least privilege on IAM roles and policies
- enable additional monitoring rules during incident window

---

## 12. Entry Vector Closure and Vulnerability Remediation

Eradication is incomplete unless initial entry is closed.

### 12.1 Common Entry Vector Closure Actions
| Vector | Closure Actions |
|-------|-----------------|
| Phishing | reset user credentials; enforce MFA; improve email controls |
| VPN compromise | reset VPN creds; enable MFA; rate limiting; patch VPN appliance |
| Exposed RDP | close internet exposure; enforce VPN/jump host; MFA |
| Web app exploit | patch; WAF rule; disable vulnerable endpoint |
| Vendor access | disable vendor accounts; restrict remote tools; rotate shared secrets |
| Supply chain | remove malicious update; rollback; verify integrity |

### 12.2 Patch and Hardening Verification
- confirm patches applied (version verified)
- confirm configuration changes are active
- confirm exposure reduced (internet-facing tests)
- document change records and approvals

---

## 13. Eradication Validation (Definition of Done)

Eradication is considered successful when all are true:

1. No ransomware payloads detected by EDR scans on cleaned/rebuilt hosts
2. No persistence mechanisms remain (verified via checks and telemetry)
3. No unauthorized accounts, tokens, or access keys remain
4. All compromised credentials have been reset and sessions revoked
5. All known C2 and exfil destinations are blocked
6. Initial access vector is remediated (patched/closed)
7. Monitoring shows no continued attacker behavior for defined window

Recommended observation window (minimum):
- P1: 24–72 hours enhanced monitoring before full return to normal
- P2: 24 hours enhanced monitoring

---

## 14. Eradication Deliverables and Documentation

Minimum documentation required:

- eradication action log
- list of cleaned/rebuilt systems and completion timestamps
- identity reset/disable log
- list of persistence mechanisms found and removed
- IOC list applied across controls
- vulnerability remediation evidence
- validation evidence (scan results, monitoring screenshots, log checks)

All documentation must be attached or referenced in the incident ticket.

---

## 15. Common Eradication Mistakes to Avoid

| Mistake | Impact | Prevention |
|--------|--------|------------|
| restoring systems before entry vector is closed | reinfection | close initial access first |
| resetting passwords without session revocation | attacker remains active | always revoke tokens/sessions |
| cleaning without persistence verification | attacker returns | verify tasks/services/run keys |
| ignoring service accounts | broad compromise | include service account reset plan |
| failing to verify backups are clean | reintroduce malware | validate backups before restore |
| poor documentation of actions | audit failure | maintain eradication log |

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Ransomware Master | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md` |
| Containment | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md` |
| Recovery | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md` |
| L3 Forensics | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| RCA Template | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md` |
| Action Tracker | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | IR Team Lead | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document