# Playbook: Data Breach and Data Exfiltration – L3 Forensics and Advanced Analysis

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Data Breach and Data Exfiltration (L3 Forensics and Advanced Analysis) |
| Document ID | IR-PB-DBR-004 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | L3 Lead / IR Team Lead |
| Approved By | CISO |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 data breach incident |

---

## 2. Purpose

This document defines the Level 3 (L3) forensic and advanced analysis
procedures for data breach and data exfiltration incidents.

L3 engagement is required when:
- large-scale exfiltration is suspected or confirmed
- the attack chain must be fully reconstructed
- regulated data exposure requires legally defensible evidence
- advanced attacker techniques are involved
- cloud and multi-system forensics are required
- legal action or regulatory investigation is anticipated

The objectives of L3 forensic analysis are to:
- reconstruct the full attack and exfiltration timeline
- identify initial access and lateral movement paths
- confirm exactly what data was accessed and exfiltrated
- identify attacker persistence and re-access capabilities
- preserve evidence to legal and regulatory standards
- support legal notifications and regulatory responses
- generate advanced detection improvements

---

## 3. Scope

Applies to:
- confirmed large-scale data exfiltration
- regulated data breach investigations
- cloud-based data exposure requiring forensics
- database compromise investigations
- API-based data extraction
- insider-driven data theft requiring advanced analysis
- multi-system or multi-cloud breach investigations
- incidents with legal or regulatory consequences

Includes:
- endpoint forensics
- cloud forensics
- database analysis
- network forensics
- identity and access forensics
- email and collaboration forensics

---

## 4. Preconditions Before L3 Investigation

L3 engagement begins after:
- L2 investigation completed
- initial scope identified
- Legal and Compliance notified
- evidence preservation confirmed

Required inputs from L2:

| Required Input | Purpose |
|---------------|---------|
| Initial scope | Data access review |
| Exposure timeline | Timeline extension |
| Exfiltration indicators | Validation |
| Affected systems | Forensic targeting |
| Cloud audit findings | Cloud review |
| User identity | Access analysis |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md`

---

# 5. L3 Investigation Objectives

| Objective | Description |
|-----------|-------------|
| Reconstruct Full Timeline | End-to-end event reconstruction |
| Confirm Data Access | Validate exactly what was accessed |
| Confirm Exfiltration | Validate data movement |
| Identify Attacker Path | Entry, movement, and exit |
| Preserve Legal Evidence | Legally defensible forensics |
| Support Regulatory Response | Regulatory investigation support |
| Improve Detection | Generate detection improvements |

---

# 6. Investigation Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | Evidence acquisition and validation |
| Phase 2 | Endpoint forensic analysis |
| Phase 3 | Network and exfiltration forensics |
| Phase 4 | Cloud and SaaS forensics |
| Phase 5 | Database and application forensics |
| Phase 6 | Identity and access forensics |
| Phase 7 | Timeline reconstruction |
| Phase 8 | Legal evidence preparation |
| Phase 9 | Detection engineering outputs |

---

# 7. Phase 1 – Evidence Acquisition and Validation

Evidence must be collected to the highest forensic standard.

---

## 7.1 Evidence Priority List

| Priority | Evidence Type |
|----------|--------------|
| Critical | Cloud audit logs |
| Critical | Database access logs |
| Critical | Network captures |
| High | Endpoint forensic image |
| High | Email audit logs |
| High | DLP export |
| Medium | Application logs |
| Medium | Identity sign-in logs |

---

## 7.2 Evidence Integrity Requirements

| Requirement | Purpose |
|-------------|---------|
| Hash all evidence | Tampering detection |
| Record collection timestamps | Chain-of-custody |
| Store in encrypted repository | Confidentiality |
| Restrict access | Need-to-know |
| Complete chain-of-custody | Legal defensibility |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

## 7.3 Log Retention Urgency

Cloud and SaaS logs frequently have short retention windows.

Priority log exports before expiry:

| Log Type | Typical Retention |
|----------|------------------|
| Azure AD Sign-in logs | 30 days |
| AWS CloudTrail | 90 days default |
| Office 365 Audit Logs | 90 days standard |
| Google Workspace | 180 days |
| Database transaction logs | Varies |

Export immediately upon L3 engagement.

---

# 8. Phase 2 – Endpoint Forensic Analysis

Endpoints may contain:
- staging artifacts
- downloaded data
- malware components
- credential theft tools

---

## 8.1 Endpoint Review Areas

| Area | Investigation Focus |
|------|--------------------|
| File system | Data staging |
| Browser artifacts | Cloud uploads |
| USB artifacts | Removable media |
| Application history | Tools used |
| Temporary directories | Staging areas |

---

## 8.2 Data Staging Indicators

| Indicator | Meaning |
|-----------|---------|
| Archive creation | Data packaging |
| Encryption tools | Concealment |
| Large temporary directories | Staging |
| Compression utilities | Pre-exfiltration |
| Bulk file copies | Collection |

---

## 8.3 Anti-Forensics Indicators

| Indicator | Meaning |
|-----------|---------|
| Log deletion | Cover-up |
| Temporary file wiping | Evidence destruction |
| Renamed tools | Masquerading |
| Cleared browser history | Concealment |

---

# 9. Phase 3 – Network and Exfiltration Forensics

This phase confirms data movement through network analysis.

---

## 9.1 Network Analysis Objectives

| Objective | Purpose |
|-----------|---------|
| Confirm external transfer | Exfiltration validation |
| Determine transfer volume | Impact quantification |
| Identify destination | Attacker infrastructure |
| Identify method | Protocol/tool analysis |
| Identify encryption | Data protection status |

---

## 9.2 Outbound Traffic Analysis

| Review Area | Purpose |
|-------------|---------|
| Proxy logs | Upload destinations |
| Firewall logs | Large outbound sessions |
| DNS logs | Suspicious domains |
| NetFlow data | Traffic volume analysis |
| DLP network captures | Content inspection |

---

## 9.3 Exfiltration Volume Estimation

| Method | Purpose |
|--------|---------|
| NetFlow volume analysis | Transfer size |
| Proxy upload records | File transfer size |
| DLP event sizes | Content size |
| Session duration analysis | Estimated volume |

---

## 9.4 Exfiltration Destination Analysis

| Indicator | Investigation Focus |
|-----------|---------------------|
| Cloud storage destination | OneDrive/Dropbox/S3 |
| Personal email | Unauthorized forwarding |
| Attacker infrastructure | Malware C2 |
| Anonymization service | VPN/Tor/proxy |

---

# 10. Phase 4 – Cloud and SaaS Forensics

Cloud forensics is critical because many breaches leverage cloud platforms.

---

## 10.1 Cloud Audit Log Analysis

| Platform | Key Audit Events |
|----------|-----------------|
| AWS | GetObject, ListBuckets, DescribeInstances |
| Azure | BlobDownload, StorageRead, ListKeys |
| GCP | Storage.objects.get, Storage.buckets.list |
| M365 | FileDownloaded, FileCopied, SharingLinkCreated |

---

## 10.2 Cloud Sharing Forensics

Review:
- sharing link creation
- external user access
- guest account invitations
- public permission changes

---

### Cloud Sharing Investigation Checklist

| Check | Purpose |
|-------|---------|
| List all public links created | Exposure scope |
| Review external user access | Unauthorized access |
| Review permission changes | Misconfiguration review |
| Review upload activity | Exfiltration validation |

---

## 10.3 OAuth and API Forensics

| Investigation Area | Purpose |
|-------------------|---------|
| OAuth consents granted | Token abuse |
| API key usage | Programmatic access |
| Service account activity | Automation abuse |
| Delegated permissions | Access review |

---

# 11. Phase 5 – Database and Application Forensics

Structured data theft from databases is common in breaches.

---

## 11.1 Database Forensic Activities

| Activity | Purpose |
|----------|---------|
| Query log review | Detect data extraction |
| Export command review | Identify dump activity |
| User privilege review | Detect unauthorized access |
| Connection log review | Identify attacker sessions |

---

## 11.2 Large Query Indicators

| Indicator | Meaning |
|-----------|---------|
| Unrestricted SELECT query | Mass data access |
| Export to file | Database dump |
| After-hours queries | Suspicious behavior |
| Unusual account running queries | Credential compromise |

---

## 11.3 Application Log Analysis

| Application | Investigation Focus |
|-------------|---------------------|
| CRM | Customer data access |
| HR System | Employee data exports |
| ERP | Financial data extraction |
| API Gateway | Programmatic extraction |

---

# 12. Phase 6 – Identity and Access Forensics

Determine how the attacker authenticated.

---

## 12.1 Identity Review Areas

| Area | Purpose |
|------|---------|
| Authentication logs | Access validation |
| Privileged account usage | Abuse detection |
| Service account activity | Automated access review |
| MFA status | Bypass indicators |
| OAuth tokens | Persistent access |

---

## 12.2 Initial Access Determination

| Vector | Evidence Source |
|--------|----------------|
| Phishing | Email logs |
| Credential stuffing | Authentication logs |
| API key theft | API logs |
| Misconfiguration | Cloud audit logs |
| Insider | Identity + endpoint |

---

## 12.3 Lateral Movement Review

| Indicator | Meaning |
|-----------|---------|
| Credential reuse | Compromised account |
| Privilege escalation | Access expansion |
| New account creation | Persistence |
| Cross-service access | Lateral movement |

---

# 13. Phase 7 – Timeline Reconstruction

Build the authoritative breach timeline.

---

## 13.1 Timeline Requirements

Include:
- initial access
- first data access
- bulk data collection
- staging activity
- exfiltration
- containment
- detection gap analysis

---

### Timeline Template

| Time (UTC) | Event | User | System | Evidence Source |
|-----------|------|------|--------|-----------------|
| | Initial access | | | |
| | Authentication | | | |
| | Data discovery | | | |
| | Bulk access | | | |
| | Data staging | | | |
| | Exfiltration | | | |
| | Detection | | | |
| | Containment | | | |

---

## 13.2 Exposure Window Determination

Critical for regulatory notifications:
- first possible exposure timestamp
- last confirmed exposure timestamp
- total exposure duration
- time to detection
- time to containment

---

# 14. Phase 8 – Legal Evidence Preparation

Data breach investigations frequently result in:
- regulatory investigations
- customer notifications
- litigation
- law enforcement referrals

Evidence must be preserved to the highest standard.

---

## 14.1 Legal Evidence Requirements

| Requirement | Purpose |
|-------------|---------|
| Chain-of-custody complete | Legal admissibility |
| Evidence hashed and validated | Integrity verification |
| All timestamps in UTC | Timeline consistency |
| Access logs maintained | Accountability |
| Evidence access restricted | Confidentiality |

---

## 14.2 Regulatory Evidence Package

Prepare:
- breach timeline document
- impacted records estimate
- evidence inventory
- exposure window confirmation
- containment actions record

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md`

---

## 14.3 Legal Notification Support

Provide Legal with:
- technical timeline
- impacted data categories
- impacted record count estimate
- exposure confirmation
- containment status

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md`

---

# 15. Phase 9 – Detection Engineering Outputs

Every data breach investigation must improve coverage.

---

## 15.1 Detection Improvement Areas

| Improvement | Purpose |
|-------------|---------|
| DLP rule tuning | Detect sensitive transfers |
| Cloud sharing alerts | Detect public exposure |
| Database export alerts | Detect extraction |
| Large outbound alerts | Detect exfiltration |
| API abuse monitoring | Detect programmatic access |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 16. Escalation Guidance

---

## 16.1 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Large-scale confirmed exfiltration | Major incident |
| Regulated data confirmed | Compliance risk |
| Multiple systems impacted | Enterprise breach |
| Advanced attacker techniques | Specialized response |

---

## 16.2 Escalate to Executive Management if:

| Condition | Reason |
|-----------|--------|
| Regulatory notification required | Executive decision |
| Customer notification required | Reputational impact |
| Legal action anticipated | Executive direction |
| Law enforcement referral | Executive approval |

---

# 17. Common L3 Investigation Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Failing to export cloud logs quickly | Log expiry |
| Not estimating record count | Regulatory underreporting |
| Incomplete timeline | Weak legal case |
| Ignoring API access logs | Missed exfiltration |
| Cleaning systems before forensics | Evidence loss |
| Not restricting evidence access | Confidentiality breach |

---

# 18. MSSP Client Handling Notes

For MSSP-managed environments:
- maintain encrypted evidence segregation
- coordinate all Legal/Compliance actions through client leadership
- avoid cross-client evidence sharing
- follow client regulatory timelines
- provide client-specific technical briefings

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 19. Related Documents

| Document | Path |
|---------|------|
| Data Breach Master | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| Data Breach L1 Triage | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md` |
| Data Breach L2 Investigation | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md` |
| Legal Notification | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md` |
| Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md` |
| Data Breach MITRE Mapping | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 20. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | L3 Lead / IR Team Lead | Initial version |

---

## 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**