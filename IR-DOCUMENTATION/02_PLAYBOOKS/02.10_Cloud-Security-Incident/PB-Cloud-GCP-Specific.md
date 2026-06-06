# Playbook: Google Cloud Platform (GCP) Security Incident Response Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Playbook – Google Cloud Platform (GCP) Security Incident Response Procedures |
| Document ID | IR-PB-GCP-001 |
| Version | 1.0 |
| Effective Date | 21-May-2026 |
| Owner | SOC Manager / Cloud Security Lead / Incident Response Team |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 GCP security incident |

---

# 2. Purpose

This playbook defines standardized procedures for responding to Google Cloud Platform (GCP) security incidents across enterprise and MSSP-managed environments.

GCP environments are highly automated and heavily dependent on IAM permissions, APIs, service accounts, and cloud-native integrations. Because GCP services are deeply interconnected, attackers can rapidly escalate privileges, access sensitive data, abuse service accounts, and move laterally across projects if containment is not performed quickly and accurately.

This document provides operational guidance for:

- GCP IAM compromise investigations
- Compute Engine compromise response
- Google Cloud Storage (GCS) exposure handling
- Service account abuse investigations
- VPC and networking containment
- Kubernetes Engine (GKE) investigations
- Cloud Audit Logs analysis
- SCC (Security Command Center) alert handling
- GCP persistence detection
- Forensic evidence preservation
- GCP eradication and recovery procedures

This playbook should be used together with the Cloud Security Incident Master Playbook during all GCP-related investigations.

---

# 3. Scope

## 3.1 In Scope

This playbook applies to incidents involving:

- Google Cloud Platform (GCP)
- GCP IAM
- Google Workspace integrations
- Compute Engine
- Google Kubernetes Engine (GKE)
- Google Cloud Storage (GCS)
- Cloud Functions
- Cloud Run
- Cloud SQL
- VPC networking
- Cloud Audit Logs
- Security Command Center (SCC)
- Secret Manager
- Cloud Build and CI/CD integrations
- Organization and project-level permissions

---

## 3.2 Typical GCP Incident Types

| Incident Type | Description |
|---|---|
| IAM Compromise | Unauthorized IAM access or abuse |
| Service Account Abuse | Compromised service account keys |
| GCS Exposure | Public bucket or object exposure |
| Compute Compromise | Malware or unauthorized VM access |
| GKE Compromise | Kubernetes cluster compromise |
| API Abuse | Unauthorized cloud API operations |
| Persistence Activity | Hidden identities or automation abuse |
| Logging Tampering | Audit logging disabled or modified |
| Data Exfiltration | Unauthorized access to cloud data |
| CI/CD Abuse | Cloud Build or deployment compromise |

---

# 4. GCP Shared Responsibility Considerations

Google secures the underlying cloud infrastructure, including physical datacenters, hardware, networking backbone, and managed platform services. Customers remain responsible for securing identities, workloads, permissions, data access, APIs, and monitoring configurations.

Security teams must understand that:

- IAM misconfigurations can expose entire projects
- Weak service account controls increase attack surface
- Public GCS buckets may expose regulated data
- Excessive API permissions enable privilege escalation
- Cloud-native automation can rapidly propagate malicious changes

Investigators must therefore focus heavily on identity activity and project-level permission changes during GCP investigations.

---

# 5. GCP Incident Detection Sources

GCP incidents may be identified using native Google security services and third-party monitoring platforms.

---

## 5.1 Native GCP Detection Sources

| Service | Purpose |
|---|---|
| Security Command Center (SCC) | Security findings and threat visibility |
| Cloud Audit Logs | Administrative and API activity |
| Cloud Logging | Operational telemetry |
| Event Threat Detection | Threat monitoring |
| VPC Flow Logs | Network activity visibility |
| Cloud Monitoring | Infrastructure telemetry |
| IAM Recommender | Permission analysis |
| Chronicle SIEM | Advanced threat detection |

---

## 5.2 Third-Party Detection Sources

Additional visibility may come from:

- SIEM platforms
- EDR telemetry
- CSPM solutions
- Threat intelligence feeds
- Kubernetes monitoring tools
- DLP systems
- MSSP monitoring infrastructure

Correlating GCP-native logs with external telemetry is critical for accurate scoping and attribution.

---

# 6. GCP Investigation Priorities

GCP investigations should prioritize identity activity, service account usage, and API operations because attackers frequently exploit these areas for persistence and lateral movement.

Investigators should immediately review:

- IAM role assignments
- Service account usage
- API enablement changes
- Cloud Audit Logs
- Project permission changes
- GCS bucket permissions
- Kubernetes activity
- VPC firewall modifications
- Cloud Build execution history

The objective is to identify how access was obtained, what permissions were abused, and whether persistence remains active.

---

# 7. GCP IAM and Service Account Compromise Investigation

Compromise of IAM identities or service accounts can allow attackers to access sensitive resources across multiple projects and services.

---

## 7.1 Common Indicators

Indicators of IAM or service account compromise include:

- Unusual API activity
- Service account key creation
- Unauthorized role assignments
- API activity from suspicious IP addresses
- Excessive failed authentication attempts
- Unusual OAuth activity
- Unauthorized privilege escalation

---

## 7.2 Investigation Steps

Investigators should:

- Review Cloud Audit Logs
- Identify recently modified IAM roles
- Audit service account permissions
- Review OAuth grant activity
- Check organization-level policy changes
- Investigate API enablement events
- Identify suspicious login activity

Special attention should be given to Owner and Editor role assignments.

---

## 7.3 Immediate Containment

Containment actions may include:

- Disabling compromised identities
- Revoking OAuth tokens
- Rotating service account keys
- Restricting IAM permissions
- Blocking suspicious IP addresses
- Enabling enhanced logging

Investigators must verify whether compromised credentials were used across multiple projects.

---

# 8. Compute Engine Compromise Investigation

Compromised Compute Engine instances may be used for persistence, malware deployment, cryptomining, lateral movement, or unauthorized access.

Investigators should determine:

- Initial access vector
- Persistence mechanisms
- Privilege escalation activity
- Network communication patterns
- Data access activity
- Malicious process execution

---

## 8.1 Common Indicators

Indicators may include:

- High CPU utilization
- Unexpected outbound traffic
- Suspicious startup scripts
- Unauthorized SSH access
- Unknown scheduled tasks
- Communication with malicious infrastructure
- Unauthorized software installation

---

## 8.2 Containment Procedures

Recommended actions include:

- Isolating affected instances
- Restricting firewall rules
- Blocking outbound communication
- Preserving disk snapshots
- Capturing runtime evidence
- Disabling unnecessary external access

Systems should not be deleted before evidence preservation activities are completed.

---

# 9. Google Cloud Storage (GCS) Exposure Investigation

Public or misconfigured GCS buckets can result in unauthorized access to sensitive or regulated data.

---

## 9.1 Common Exposure Scenarios

| Scenario | Example |
|---|---|
| Public bucket exposure | Internet-accessible bucket |
| Anonymous object access | Unrestricted file visibility |
| Excessive IAM permissions | Overly permissive access |
| Cross-project exposure | Unauthorized project access |

---

## 9.2 Investigation Priorities

Investigators must determine:

- Whether sensitive data was exposed
- Which files or objects were accessed
- Whether external downloads occurred
- How long exposure existed
- Whether attacker persistence exists

Critical evidence sources include:

- Cloud Audit Logs
- GCS access logs
- SCC findings
- IAM policy history

---

## 9.3 Immediate Containment

Containment activities may include:

- Removing public access
- Restricting bucket permissions
- Revoking shared access
- Preserving access logs
- Enabling enhanced monitoring

Legal and Compliance teams must be notified immediately if regulated data exposure is confirmed.

---

# 10. GCP Persistence Mechanisms

Attackers frequently establish persistence within GCP using identities, APIs, and automation services.

Common persistence techniques include:

- Rogue IAM users
- Malicious service account keys
- Unauthorized API enablement
- Cloud Function persistence
- Hidden project permissions
- Startup script abuse
- CI/CD pipeline compromise

Investigators must carefully audit all recently modified IAM and automation configurations.

---

# 11. Cloud Audit Logs Investigation

Cloud Audit Logs are among the most important evidence sources during GCP investigations.

These logs help investigators identify:

- API operations
- Administrative activity
- Permission changes
- Resource modifications
- Timeline reconstruction
- Logging tampering attempts

---

## 11.1 Key Audit Events

| Event Type | Importance |
|---|---|
| SetIamPolicy | Privilege escalation |
| CreateServiceAccountKey | Credential creation |
| storage.setIamPermissions | Storage exposure |
| compute.instances.start | Unauthorized compute activity |
| logging.sinks.update | Logging tampering |
| serviceusage.services.enable | Unauthorized API enablement |

---

## 11.2 Logging Integrity Checks

Investigators must verify:

- Audit logging remained enabled
- Logs were not deleted
- Export pipelines remained operational
- SIEM forwarding succeeded

Any evidence of logging tampering significantly increases incident severity.

---

# 12. Security Command Center (SCC) Investigation

Security Command Center provides native GCP threat visibility and posture monitoring.

Common SCC findings include:

- Public storage exposure
- IAM misconfigurations
- Malware activity
- Cryptomining behavior
- Excessive permissions
- API abuse

SCC findings should always be correlated with Audit Logs and network telemetry.

---

# 13. Google Kubernetes Engine (GKE) Investigation

Compromise of GKE clusters may expose workloads, APIs, secrets, and cloud identities.

---

## 13.1 Investigation Focus Areas

Investigators should review:

- Kubernetes audit logs
- Cluster role bindings
- Service account permissions
- Container runtime activity
- Secret access events
- Pod execution activity
- Workload identity usage

---

## 13.2 Containment Actions

Containment actions may include:

- Isolating namespaces
- Cordoning affected nodes
- Removing malicious workloads
- Rotating secrets
- Restricting cluster API access

Investigators must determine whether GCP IAM permissions linked to Kubernetes workloads were abused.

---

# 14. GCP Network Containment

GCP network containment relies on VPC firewall rules, segmentation, and flow monitoring.

Containment activities may include:

- Blocking malicious IP addresses
- Restricting ingress access
- Restricting outbound traffic
- Applying quarantine firewall rules
- Enabling enhanced VPC Flow Logs

All network modifications must be documented and approved through incident management procedures.

---

# 15. GCP Forensic Evidence Collection

Evidence preservation is critical during GCP investigations because cloud-native telemetry can be modified or deleted rapidly.

---

## 15.1 Critical Evidence Sources

| Evidence Type | Examples |
|---|---|
| Administrative logs | Cloud Audit Logs |
| Workload evidence | Disk snapshots |
| Storage telemetry | GCS access logs |
| Networking telemetry | VPC Flow Logs |
| IAM evidence | Role assignments and keys |
| Kubernetes evidence | GKE audit logs |

---

## 15.2 Evidence Preservation Requirements

Investigators must:

- Export logs securely
- Preserve snapshots
- Record timestamps in UTC
- Hash exported evidence
- Maintain chain-of-custody documentation

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 16. GCP Eradication Guidance

After containment is validated, eradication activities should remove persistence mechanisms and restore trusted configurations.

Typical eradication actions include:

- Removing malicious IAM roles
- Rotating service account keys
- Rebuilding compromised instances
- Restricting excessive permissions
- Hardening storage configurations
- Disabling unauthorized APIs
- Updating firewall controls

All eradication activities must be documented.

---

# 17. GCP Recovery Guidance

Recovery activities should ensure workloads are securely restored and monitoring capabilities remain operational.

Recovery validation should confirm:

- Logging is operational
- IAM permissions are hardened
- Persistence mechanisms removed
- Monitoring restored
- Security baselines re-applied
- Sensitive data integrity validated

Enhanced monitoring should remain enabled after recovery.

---

# 18. MSSP GCP Considerations

For MSSP-managed GCP environments:

- Shared administration increases blast radius
- Client evidence segregation is mandatory
- Tenant isolation must be validated
- Separate communication timelines may apply
- Shared automation pipelines require additional review

Any compromise involving shared management infrastructure must be escalated immediately.

---

# 19. Regulatory and Compliance Considerations

GCP incidents involving sensitive or regulated data may trigger:

- RBI reporting obligations
- CERT-In notification requirements
- Client contractual notification obligations
- Data breach reporting requirements
- ISO 27001 audit review

Legal and Compliance teams must remain involved throughout major investigations.

---

# 20. Related Documents

| Document | Path |
|---|---|
| Cloud Master Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md` |
| Cloud Containment Procedures | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Containment.md` |
| Cloud L1 Triage | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md` |
| Cloud L2 Investigation | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md` |
| Cloud L3 Forensics | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L3-Forensics.md` |
| Cloud AWS Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-AWS-Specific.md` |
| Cloud Azure Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Azure-Specific.md` |
| Cloud MITRE Mapping | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-MITRE-Mapping.md` |
| Evidence Handling Procedures | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

# 21. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 21-May-2026 | SOC Manager / Cloud Security Lead / Incident Response Team | Initial version |

---

# 22. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**