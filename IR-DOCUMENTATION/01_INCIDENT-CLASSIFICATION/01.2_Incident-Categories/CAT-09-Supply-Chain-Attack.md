# CAT-09 – Supply Chain Attack Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Supply Chain Attack |
| Document ID | IR-CAT-009 |
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
| Category ID | CAT-09 |
| Default Severity | P1 – Critical (production compromise or widespread exposure) / P2 – High (suspected compromise of trusted vendor/software) |
| Escalation Priority | Immediate due to uncertainty of scope and multi-tenant/client impact (MSSP) |
| Attack Goal | Compromise trusted supplier, software, update mechanism, or service provider to access victim environments |
| Threat Actors | APT groups, ransomware affiliates, advanced cybercriminals |
| Playbook Reference | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/` |

---

## 3. What is a Supply Chain Attack?

A supply chain attack is an incident where an attacker compromises a
trusted third-party component or relationship in order to impact the
target organization indirectly.

Supply chain attacks commonly target:

- Software vendors and update servers
- Managed service providers (MSPs/MSSPs)
- Open-source libraries and dependencies
- Hardware vendors and firmware
- Cloud/SaaS service providers
- CI/CD pipelines and build systems
- Third-party integrations with privileged access

These incidents are high risk because they can bypass traditional
perimeter defenses and spread to multiple customers/tenants.

---

## 4. Supply Chain Attack Types

| Type | Description |
|------|-------------|
| Compromised Software Update | Malicious code inserted into vendor update package |
| Dependency Hijacking | Compromise of open-source dependency used by applications |
| Code Signing Abuse | Use of legitimate or stolen certificates to sign malware |
| Build Pipeline Compromise | Compromise of CI/CD tools and build artifacts |
| Vendor Account Compromise | Attacker uses vendor credentials to access customer systems |
| Managed Service Provider Compromise | Attacker gains access through MSP tools (RMM, scripting) |
| Hardware/Firmware Tampering | Compromise of firmware or hardware components |
| Cloud Service Compromise | Abuse of SaaS integrations or cloud provider accounts |

---

## 5. Common Scenarios

| Scenario | Description |
|---------|-------------|
| Trojanized Update | Vendor patch/update contains malicious payload |
| RMM Tool Abuse | Remote management tool used to deploy malware to endpoints |
| Compromised API Integration | Third-party integration used to access data or change configurations |
| Credential Theft at Vendor | Vendor support account compromised and used for access |
| Library Backdoor | Open-source package updated with malicious backdoor |
| Compromised Container Images | Malicious container image pulled into production |
| Compromised SSO Federation | Trust relationship exploited via identity federation |

---

## 6. Indicators of Supply Chain Compromise (IoCs and Observables)

### 6.1 Vendor / Update Indicators

| Indicator | Details |
|----------|---------|
| Unexpected Update | Update installed outside normal change window |
| Hash Mismatch | Update package hash does not match expected vendor hash |
| Certificate Anomaly | Update signed by unexpected or revoked certificate |
| New Executables After Update | New binaries/services created after patching |
| Unexpected Persistence | Scheduled tasks/services created after update |

### 6.2 Endpoint / Server Indicators

| Indicator | Details |
|----------|---------|
| RMM Execution | Remote management agent executing scripts unexpectedly |
| Mass Deployment | Same payload deployed across many systems simultaneously |
| New Admin Accounts | Accounts created after vendor support session |
| Unusual Privileged Actions | Privileged commands executed using vendor accounts |
| C2 Communication | New outbound communications appearing after update |

### 6.3 Network / Cloud Indicators

| Indicator | Details |
|----------|---------|
| Vendor IP Activity | Unusual connections to vendor networks not typical for environment |
| API Abuse | Unusual API calls from third-party integration |
| SaaS Token Creation | New tokens or app credentials created unexpectedly |
| Data Access Patterns | Large data access volume from integration accounts |

### 6.4 Key Log Sources

| Source | What to Look For |
|--------|------------------|
| EDR Telemetry | New processes, mass deployments, RMM usage |
| Patch Management Logs | Update timeline, package details, hash verification |
| CI/CD Logs | Build and deployment history, artifact integrity |
| IAM Logs | Vendor account activity, token creation, privilege assignments |
| Cloud Audit Logs | Third-party integration behavior, admin actions |
| Firewall/Proxy Logs | C2 communication and abnormal outbound traffic |
| Vendor Notifications | Security advisories, compromise statements, IOCs |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Confirmed malicious vendor update deployed in production | P1 – Critical |
| Confirmed compromise of MSP/RMM tool impacting multiple systems | P1 – Critical |
| Confirmed cross-client/tenant exposure (MSSP multi-tenant) | P1 – Critical |
| Confirmed data breach originating from vendor integration | P1 – Critical |
| Suspected vendor compromise with credible indicators (IOC match, abnormal update) | P2 – High |
| Compromise limited to non-production/test environment | P2 – High |
| Suspicious vendor activity requiring validation | P3 – Medium |
| Vendor advisory received with no exposure evidence | P4 – Low |

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes

- Create incident ticket and assign initial severity based on exposure
- Notify SOC Lead immediately for P2 and above
- Identify affected vendor/product/service and version(s) involved
- Determine whether the affected component is deployed in production
- Preserve evidence:
  - update packages
  - hashes and signatures
  - deployment logs
  - endpoint telemetry
- Temporarily pause further deployments or updates (change control approval)
- Start scoping: identify all systems with the affected component installed

### 8.2 First 1 Hour

- Validate update integrity:
  - hash checks
  - certificate/signature validation
  - compare with vendor known-good indicators
- Identify impact:
  - processes created post-update
  - new services/tasks
  - outbound network communications
- Block known IOCs from vendor advisory (domains/IPs/hashes)
- Engage vendor support/security team using formal communication channel
- Engage IR Team if production exposure is confirmed or suspected
- For MSSP: assess whether multiple clients are affected and enforce segregation

### 8.3 First 4 Hours

- Confirm scope across enterprise/client environments:
  - endpoints
  - servers
  - cloud integrations
  - SaaS tenants
- Implement containment:
  - isolate systems showing suspicious behavior
  - disable compromised vendor accounts/integration tokens
  - restrict vendor access paths temporarily
- Begin eradication:
  - remove malicious components
  - roll back to known good versions (if safe)
  - rotate credentials, API keys, and certificates if exposed
- Prepare management status update and client communications (MSSP)

---

## 9. Containment and Eradication Guidance

| Action | Purpose | Notes |
|-------|---------|------|
| Pause Updates/Deployments | Stop further spread | Use change management; document approval |
| Block Vendor IOCs | Prevent C2 and further compromise | Implement in SIEM/EDR/firewall/proxy |
| Disable Vendor Access | Prevent further unauthorized support sessions | Review contracts and access mechanisms |
| Rotate Integration Tokens | Cut off attacker access | Coordinate with application owners |
| Remove Malicious Components | Eliminate persistence | Preserve evidence first |
| Rollback / Rebuild | Restore trusted state | Prefer rebuild for high-risk components |
| Increase Monitoring | Detect follow-on activities | Threat hunting recommended |

---

## 10. MITRE ATT&CK Mapping

Supply chain incidents may involve multiple technique sets. Common mappings include:

| Tactic | Technique | ID |
|--------|-----------|----|
| Initial Access | Supply Chain Compromise | T1195 |
| Initial Access | Trusted Relationship | T1199 |
| Execution | Command and Scripting Interpreter | T1059 |
| Persistence | Create or Modify System Process | T1543 |
| Defense Evasion | Signed Binary Proxy Execution | T1218 |
| Credential Access | Valid Accounts | T1078 |
| Lateral Movement | Remote Services | T1021 |
| Command and Control | Application Layer Protocol | T1071 |
| Exfiltration | Exfiltration Over Web Service | T1567 |
| Impact | Data Encrypted for Impact | T1486 |

---

## 11. Key Investigation Questions

1. Which vendor/product/service is involved?
2. What versions are impacted and where are they deployed?
3. Is the component in production and business-critical?
4. Was an update installed recently, and was it expected?
5. Do hashes and signatures match vendor known-good values?
6. Are there new processes/services/tasks created post-update?
7. Is there evidence of external communication to suspicious destinations?
8. Are vendor accounts or integration tokens being abused?
9. How many systems/clients are impacted (MSSP context)?
10. Is there evidence of data access or exfiltration?
11. What is the vendor’s official incident status and provided IOCs?
12. What immediate actions stop spread without causing additional business outage?
13. Is full rebuild required for affected systems?

---

## 12. Critical Do's and Do Not's

### Do

- Treat early indicators seriously; scope may be larger than visible
- Preserve update artifacts and deployment logs for evidence
- Validate vendor communications through trusted channels
- Use coordinated communication to avoid misinformation
- Enforce tenant separation and client confidentiality (MSSP)
- Rotate keys/tokens and restrict trusted integrations if exposure suspected
- Document all containment decisions and approvals

### Do Not

- Trust vendor-provided binaries without validation of hashes and signatures
- Continue deployments during active investigation
- Allow unrestricted vendor access during suspected compromise
- Assume only one client is affected in MSSP environments
- Close incident without a full scope assessment across assets and integrations

---

## 13. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Identify vendor-related alert/advisory and open ticket |
| L2 Investigation | Validate exposure, scope installed base, check logs |
| SOC Lead | Coordinate response, approve severity and communications |
| IR Team | Lead containment/forensics for production exposure |
| Vendor Management / Procurement | Coordinate vendor engagement and contractual actions |
| Application Owners / DevOps | Pause deployments, rollback versions, rotate secrets |
| GRC / Compliance | Assess regulatory impact if breach confirmed |
| Legal | Guide vendor communication, liability, and disclosure |
| Management / CISO | Approve major actions and external messaging |
| MSSP SDM / Client Owners | Coordinate multi-client scope and notifications |

---

## 14. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Confirmed breach impacting customer/regulated data | Engage Compliance and Legal; assess reporting |
| Cross-client exposure (MSSP) | Notify affected clients per SLA and contract |
| Critical infrastructure impact | Assess CERT-In / sector reporting requirements |
| Vendor compromise impacts security controls | Consider additional audit evidence collection |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| Update package files | Critical | Preserve original binaries and installers |
| Hash and signature verification results | Critical | Document method and results |
| Patch management logs | Critical | Installation timestamps and target hosts |
| Endpoint EDR telemetry | High | Process trees and file modifications |
| Network logs | High | Outbound destinations and traffic patterns |
| IAM logs | High | Vendor account use, token creation, privilege changes |
| CI/CD logs | High | Build artifacts and deployment history |
| Cloud audit logs | High | Third-party integration behaviors |
| Vendor advisories and communications | Medium | Preserve official statements and IOCs |
| Chain-of-custody forms | As needed | Required for legal-grade evidence |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Supply Chain Master Playbook | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L2-Investigation.md` |
| L3 Forensics Playbook | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L3-Forensics.md` |
| Vendor Coordination | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Vendor-Coordination.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-MITRE-Mapping.md` |
| Third-Party Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md` |
| P1 Critical Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**