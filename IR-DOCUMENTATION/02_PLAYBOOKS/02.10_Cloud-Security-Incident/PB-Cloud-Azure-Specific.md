# Playbook: Microsoft Azure Cloud Security Incident Response Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Playbook – Microsoft Azure Cloud Security Incident Response Procedures |
| Document ID | IR-PB-AZR-001 |
| Version | 1.0 |
| Effective Date | 21-May-2026 |
| Owner | SOC Manager / Cloud Security Lead / Incident Response Team |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 Azure security incident |

---

# 2. Purpose

This playbook defines standardized procedures for responding to Microsoft Azure cloud security incidents across enterprise and MSSP-managed Azure environments.

Azure environments rely heavily on identity-driven access control, cloud-native automation, and integrated services such as Microsoft Entra ID, Azure Resource Manager (ARM), Microsoft Defender for Cloud, and Microsoft Sentinel. Because Azure services are deeply interconnected, a compromise affecting a privileged identity or management subscription can rapidly impact multiple workloads and business-critical services.

This document provides detailed guidance for:

- Azure identity compromise investigations
- Azure VM compromise response
- Azure storage exposure handling
- Azure networking containment
- Azure persistence detection
- Azure Activity Log investigations
- Azure Kubernetes Service (AKS) investigations
- Azure automation and DevOps abuse investigations
- Microsoft Defender for Cloud alert handling
- Azure forensic evidence preservation
- Azure eradication and recovery procedures

This playbook supplements the master cloud security incident response procedures and should be used for all Azure-specific investigations.

---

# 3. Scope

## 3.1 In Scope

This playbook applies to incidents involving:

- Microsoft Azure subscriptions
- Microsoft Entra ID (Azure AD)
- Azure Virtual Machines
- Azure Blob Storage
- Azure Kubernetes Service (AKS)
- Azure Functions
- Azure Resource Manager (ARM)
- Azure Key Vault
- Azure Networking
- Azure Firewall
- Microsoft Sentinel
- Microsoft Defender for Cloud
- Azure DevOps
- Azure Monitor
- Azure Policy
- Azure Automation

---

## 3.2 Typical Azure Incident Types

| Incident Type | Description |
|---|---|
| Identity Compromise | Entra ID or privileged account abuse |
| Azure VM Compromise | Malware or unauthorized access |
| Storage Exposure | Public Blob exposure |
| Azure API Abuse | Malicious ARM operations |
| AKS Compromise | Kubernetes cluster compromise |
| OAuth Abuse | Token theft or federation abuse |
| Persistence Activity | Unauthorized automation or identities |
| Logging Tampering | Azure logging disabled |
| Data Exfiltration | Unauthorized data access or transfer |
| DevOps Compromise | Azure DevOps abuse |

---

# 4. Azure Shared Responsibility Considerations

Microsoft secures the underlying Azure infrastructure, including physical datacenters, networking backbone, and managed platform services. Customers remain responsible for configuring and securing identities, workloads, applications, storage permissions, and monitoring capabilities.

Security teams must understand that:

- Misconfigured RBAC permissions can expose critical services
- Weak Conditional Access policies increase attack risk
- Improper Blob access settings may expose sensitive data
- Azure automation can propagate malicious changes rapidly
- Entra ID compromise can affect both cloud and hybrid environments

Investigators must therefore review both infrastructure activity and identity-related changes during all Azure incident investigations.

---

# 5. Azure Incident Detection Sources

Azure incidents may be identified through multiple telemetry sources and cloud-native security tools.

---

## 5.1 Native Azure Detection Sources

| Service | Purpose |
|---|---|
| Microsoft Defender for Cloud | Threat detection and posture monitoring |
| Azure Activity Logs | Administrative operations |
| Microsoft Sentinel | SIEM and analytics |
| Entra ID Sign-In Logs | Authentication activity |
| Azure Monitor | Operational telemetry |
| Azure Policy | Configuration monitoring |
| Defender for Identity | Identity attack detection |
| Defender for Endpoint | Endpoint telemetry |

---

## 5.2 Third-Party Detection Sources

Additional visibility may come from:

- SIEM platforms
- EDR telemetry
- CSPM tools
- Threat intelligence feeds
- Kubernetes runtime monitoring
- DLP systems
- MSSP monitoring infrastructure

Correlation between Azure-native and third-party telemetry is critical for accurate scoping.

---

# 6. Azure Investigation Priorities

Azure investigations should prioritize identity and management plane activity because attackers frequently target Entra ID accounts and Azure Resource Manager operations.

Investigators should immediately review:

- Privileged account activity
- Role assignments
- OAuth grants
- Conditional Access modifications
- Resource deployment activity
- Storage access
- Azure networking changes
- Newly created service principals
- Azure automation activity

The objective is to determine how access was obtained, which permissions were abused, and whether attacker persistence remains active.

---

# 7. Entra ID (Azure AD) Compromise Investigation

Compromise of Entra ID accounts can provide attackers with extensive access across cloud and hybrid environments.

---

## 7.1 Common Indicators

Indicators of identity compromise may include:

- Impossible travel logins
- MFA fatigue or bypass attempts
- Unauthorized OAuth consent grants
- Suspicious token activity
- Excessive failed authentication attempts
- Privileged role assignment changes
- Login activity from malicious IP addresses

---

## 7.2 Investigation Steps

Investigators should:

- Review Sign-In Logs
- Review Audit Logs
- Identify newly granted permissions
- Review Conditional Access changes
- Audit privileged roles
- Identify unauthorized applications
- Review token issuance events
- Investigate suspicious service principals

---

## 7.3 Immediate Containment

Containment actions may include:

- Disabling compromised accounts
- Revoking active sessions
- Blocking sign-in activity
- Resetting credentials
- Removing malicious OAuth grants
- Restricting privileged access
- Enabling enhanced monitoring

Special attention should be given to Global Administrator activity because compromise at this level may affect all Azure services.

---

# 8. Azure VM Compromise Investigation

Compromised Azure Virtual Machines may be used for malware deployment, persistence, lateral movement, or unauthorized remote access.

Investigators should focus on identifying:

- Initial compromise vector
- Persistence mechanisms
- Privilege escalation
- Outbound communication
- Unauthorized software execution
- Data access activity

---

## 8.1 Common Indicators

Indicators may include:

- Unusual CPU or network activity
- Unauthorized RDP or SSH access
- New administrative accounts
- Suspicious PowerShell execution
- Malware detections
- Azure extension abuse
- Unexpected scheduled tasks

---

## 8.2 Containment Procedures

Recommended actions include:

- Isolating Azure VMs
- Restricting NSG rules
- Blocking outbound traffic
- Preserving VM snapshots
- Capturing volatile evidence
- Restricting internet connectivity

Affected systems should not be deleted before evidence collection is completed.

---

# 9. Azure Storage Exposure Investigation

Azure Blob Storage exposure incidents can result in unauthorized data access and regulatory reporting obligations.

---

## 9.1 Common Exposure Scenarios

| Scenario | Example |
|---|---|
| Public Blob access | Internet-accessible containers |
| Weak SAS tokens | Excessive sharing permissions |
| Misconfigured RBAC | Unauthorized storage access |
| Anonymous access enabled | Unrestricted object visibility |

---

## 9.2 Investigation Priorities

Investigators must determine:

- Whether sensitive data was exposed
- Which objects were accessed
- Whether external downloads occurred
- How long exposure existed
- Whether attacker persistence exists

Critical evidence sources include:

- Storage Analytics Logs
- Azure Monitor logs
- Azure Activity Logs
- Defender for Cloud findings

---

## 9.3 Immediate Containment

Containment actions may include:

- Disabling public access
- Revoking SAS tokens
- Restricting RBAC permissions
- Preserving access logs
- Enabling enhanced monitoring

If regulated data is involved, Legal and Compliance teams must be notified immediately.

---

# 10. Azure Persistence Mechanisms

Attackers frequently establish persistence within Azure environments using cloud-native services and automation.

Common persistence techniques include:

- Malicious service principals
- Unauthorized OAuth applications
- Persistent access tokens
- Azure Automation runbooks
- Azure Functions abuse
- Hidden privileged role assignments
- ARM template persistence

Investigators must review all recently modified identity and automation configurations.

---

# 11. Azure Activity Log Investigation

Azure Activity Logs provide critical evidence for identifying administrative and management plane activity.

These logs help investigators determine:

- Who performed actions
- Which resources were modified
- Whether logging was disabled
- Which subscriptions were affected
- Timeline reconstruction

---

## 11.1 Key Activity Types

| Event Type | Importance |
|---|---|
| Role Assignment Changes | Privilege escalation |
| Resource Deployment | Unauthorized infrastructure |
| NSG Changes | Network exposure |
| Storage Configuration Changes | Data exposure |
| Logging Changes | Anti-forensics |
| Application Consent Grants | OAuth abuse |

---

## 11.2 Logging Integrity Checks

Investigators must verify:

- Diagnostic logging remained enabled
- Log retention was not modified
- Sentinel ingestion remained operational
- Log forwarding succeeded

Any logging tampering significantly increases incident severity.

---

# 12. Microsoft Defender for Cloud Investigation

Microsoft Defender for Cloud provides native Azure threat detection and security posture visibility.

Common alert categories include:

- Identity compromise
- Malware detection
- Cryptomining activity
- Network reconnaissance
- Lateral movement
- Vulnerability exploitation

All alerts should be correlated with Activity Logs and Sign-In Logs.

---

# 13. Azure Kubernetes Service (AKS) Investigation

Compromise of AKS environments may expose workloads, secrets, APIs, and cloud identities.

---

## 13.1 Investigation Focus Areas

Investigators should review:

- Kubernetes audit logs
- Cluster role bindings
- Service accounts
- Secret access
- Container images
- Pod execution activity
- Azure AD integration

---

## 13.2 Containment Actions

Containment actions may include:

- Isolating namespaces
- Cordoning nodes
- Removing malicious workloads
- Rotating Kubernetes secrets
- Restricting API access

Investigators must determine whether managed identities associated with AKS were abused.

---

# 14. Azure Network Containment

Azure network containment relies heavily on NSGs, Azure Firewall, routing controls, and segmentation.

Containment activities may include:

- Blocking malicious IP addresses
- Restricting inbound connectivity
- Restricting outbound communication
- Applying quarantine NSGs
- Enabling enhanced flow logging

All network changes must be documented and approved through incident management procedures.

---

# 15. Azure Forensic Evidence Collection

Azure evidence collection must preserve cloud-native telemetry and workload evidence before resources are modified.

---

## 15.1 Critical Evidence Sources

| Evidence Type | Examples |
|---|---|
| Administrative logs | Azure Activity Logs |
| Authentication telemetry | Entra ID Sign-In Logs |
| Workload evidence | VM snapshots |
| Networking telemetry | NSG Flow Logs |
| Storage telemetry | Blob access logs |
| Kubernetes evidence | AKS audit logs |

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

# 16. Azure Eradication Guidance

After containment is validated, eradication activities should remove persistence and restore trusted configurations.

Typical eradication actions include:

- Removing malicious service principals
- Revoking OAuth grants
- Rotating credentials
- Rebuilding compromised VMs
- Hardening RBAC permissions
- Updating NSGs
- Patching vulnerable systems

All eradication activities must be documented within the incident record.

---

# 17. Azure Recovery Guidance

Recovery activities should ensure workloads are restored securely and monitoring visibility is maintained.

Recovery validation should confirm:

- Logging is operational
- Identity controls are hardened
- Persistence mechanisms removed
- Monitoring restored
- Security baselines applied
- Sensitive data integrity validated

Enhanced monitoring should remain enabled after recovery.

---

# 18. MSSP Azure Considerations

For MSSP-managed Azure environments:

- Shared management subscriptions increase risk exposure
- Cross-client segregation must be maintained
- Client evidence handling must remain isolated
- Separate client notification timelines may apply
- Shared automation platforms require additional review

Any compromise affecting shared infrastructure must be escalated immediately.

---

# 19. Regulatory and Compliance Considerations

Azure incidents involving sensitive data may trigger:

- RBI reporting requirements
- CERT-In notification obligations
- Client contractual reporting
- Data breach notification requirements
- ISO 27001 audit review

Legal and Compliance teams must remain engaged throughout major incident handling.

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
| Cloud GCP Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-GCP-Specific.md` |
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