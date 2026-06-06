# Playbook: Cloud Security Incident Containment Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Playbook – Cloud Security Incident Containment Procedures |
| Document ID | IR-PB-CLD-005 |
| Version | 1.0 |
| Effective Date | 21-May-2026 |
| Owner | SOC Manager / Cloud Security Lead / Incident Response Team |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 cloud security incident |

---

# 2. Purpose

This playbook defines the standardized containment procedures for cloud security incidents affecting enterprise cloud environments and MSSP-managed infrastructure. The purpose of containment is to rapidly stop malicious activity, minimize operational disruption, reduce attacker persistence opportunities, and prevent further compromise while preserving forensic evidence required for investigation and regulatory reporting.

Unlike traditional on-premises incidents, cloud incidents evolve rapidly because cloud environments are API-driven, highly scalable, identity-centric, and often globally distributed. A compromised IAM credential, exposed storage bucket, or abused automation pipeline can lead to large-scale impact within minutes. As a result, containment actions in cloud environments must be carefully coordinated to avoid unintended business outages or destruction of critical forensic evidence.

This playbook provides structured guidance for:

- Immediate cloud threat containment
- IAM compromise response
- Cloud workload isolation
- Public exposure remediation
- Data exfiltration prevention
- Kubernetes and container isolation
- Cross-account compromise handling
- Preservation of cloud-native forensic evidence
- Multi-cloud incident coordination
- MSSP multi-tenant containment operations

The procedures defined in this document support AWS, Microsoft Azure, Google Cloud Platform (GCP), and hybrid cloud environments.

---

# 3. Scope

## 3.1 In Scope

This playbook applies to all cloud security incidents involving:

- AWS environments
- Microsoft Azure environments
- Google Cloud Platform (GCP)
- Hybrid cloud deployments
- Multi-cloud infrastructure
- Cloud IAM systems
- Kubernetes and container platforms
- Serverless technologies
- Cloud-native storage services
- Cloud networking components
- MSSP-managed cloud environments

The playbook also applies to incidents involving:

- Stolen API keys
- OAuth token compromise
- Public storage exposure
- Cloud malware or cryptomining
- Cloud workload compromise
- Cloud persistence mechanisms
- Unauthorized cloud API activity
- Cross-account attacks
- Data exfiltration from cloud storage
- CI/CD compromise

---

## 3.2 Out of Scope

The following scenarios should be handled using separate dedicated playbooks:

| Scenario | Referenced Playbook |
|---|---|
| Traditional phishing attacks | 02.2_Phishing-BEC/ |
| On-premises-only intrusions | 02.11_Network-Intrusion/ |
| Pure web application attacks | 02.8_Web-Application-Attack/ |
| Supply chain compromise investigations | 02.9_Supply-Chain-Attack/ |

---

# 4. Containment Objectives

The primary goal of cloud containment is to immediately reduce attacker capability while maintaining operational stability and preserving evidence integrity.

Cloud containment activities are designed to:

- Stop active malicious activity
- Prevent lateral movement across cloud resources
- Restrict unauthorized access
- Preserve critical forensic artifacts
- Minimize customer and business impact
- Prevent additional data exposure
- Stabilize affected cloud environments
- Support legal and regulatory obligations

Containment should always be proportional to the severity and scope of the incident. Overly aggressive actions may unintentionally destroy evidence or cause significant production outages. Therefore, all containment activities must balance operational continuity with security risk reduction.

---

# 5. Roles and Responsibilities

Successful cloud containment requires coordinated execution across multiple operational and security teams.

| Role | Responsibility |
|---|---|
| L1 Analyst | Initial alert validation and escalation |
| L2 Analyst | Scope assessment and containment recommendations |
| L3 Analyst | Advanced technical containment support |
| Cloud Security Team | Execution of cloud-native controls |
| SOC Lead | Incident coordination and approvals |
| Incident Response Team | Major incident management |
| IAM Team | Identity and access containment |
| Network Team | Traffic restriction and segmentation |
| DevOps Team | CI/CD and automation review |
| Compliance Team | Regulatory coordination |
| MSSP Operations | Multi-client coordination |

The SOC Lead is responsible for ensuring containment activities are properly documented, approved, and communicated to stakeholders.

---

# 6. Cloud Containment Principles

Cloud environments require a fundamentally different containment strategy compared to traditional infrastructure. Because resources can be provisioned, modified, or deleted rapidly through APIs and automation pipelines, containment procedures must follow strict operational principles.

---

## 6.1 Preserve Evidence Before Destructive Actions

One of the most common mistakes during cloud incidents is deleting compromised resources too early. Cloud systems may contain valuable forensic evidence such as attacker tooling, persistence scripts, temporary credentials, API activity, or memory-resident malware.

Before destructive actions are taken, responders should:

- Export critical cloud logs
- Snapshot affected workloads
- Preserve IAM configurations
- Capture active network connections
- Record timestamps and cloud regions
- Preserve storage access logs

Resources should not be terminated unless explicitly approved by the Incident Response Lead or SOC Manager.

---

## 6.2 Prioritize Identity Containment

In cloud environments, identity is often the primary security boundary. Attackers frequently rely on compromised IAM users, OAuth grants, access keys, or federation abuse to maintain persistence.

Containment activities should therefore prioritize:

- Revoking active sessions
- Disabling compromised identities
- Rotating exposed credentials
- Reviewing privilege escalation
- Removing unauthorized trust relationships
- Auditing recently created accounts or roles

Failure to fully contain identity compromise can allow attackers to quickly re-establish access even after workloads are rebuilt.

---

## 6.3 Minimize Operational Disruption

Cloud environments often host business-critical production systems. Containment actions must therefore avoid unnecessary outages whenever possible.

Preferred actions include:

- Isolating individual workloads instead of entire environments
- Restricting specific IAM permissions instead of broad lockouts
- Blocking malicious traffic selectively
- Applying temporary segmentation controls
- Restricting internet access while maintaining internal communication

All high-impact containment actions affecting production services must be approved through the incident bridge process.

---

## 6.4 Assume Persistence Exists

Cloud attackers frequently establish persistence using cloud-native mechanisms. Even after initial access is removed, persistence may remain hidden within automation or identity configurations.

Investigators must review:

- Newly created IAM users
- Unauthorized access keys
- Federation trust relationships
- Startup scripts
- Scheduled automation
- Serverless functions
- Kubernetes service accounts
- CI/CD pipeline modifications

Containment is not considered successful until persistence mechanisms are identified and removed.

---

## 6.5 Validate Logging Integrity

Sophisticated attackers may attempt to disable cloud logging to reduce visibility and hinder investigations.

During containment, teams must validate:

- CloudTrail status in AWS
- Azure Activity Log retention
- GCP Audit Logging configuration
- SIEM integrations
- CSPM visibility
- Log forwarding pipelines

If logging gaps are identified, enhanced monitoring should be enabled immediately.

---

# 7. Cloud Containment Workflow

Cloud containment activities should follow a structured workflow to ensure consistency, accountability, and evidence preservation.

| Phase | Description |
|---|---|
| Phase 1 | Validate incident |
| Phase 2 | Assess impact |
| Phase 3 | Preserve evidence |
| Phase 4 | Execute containment |
| Phase 5 | Validate containment |
| Phase 6 | Transition to eradication |

Each phase must be documented within the incident ticketing system.

---

# 8. Initial Containment Decision Matrix

Containment actions should be selected based on the nature and severity of the cloud incident.

| Scenario | Recommended Immediate Action |
|---|---|
| IAM compromise | Disable account and revoke sessions |
| Public storage exposure | Remove public access immediately |
| Active data exfiltration | Block outbound communication |
| Malware or cryptomining | Isolate affected workloads |
| Kubernetes compromise | Isolate nodes and namespaces |
| API abuse | Disable API tokens and keys |
| Cross-account compromise | Remove trust relationships |
| Unauthorized automation | Disable CI/CD pipelines temporarily |

These actions may require emergency approval depending on business impact.

---

# 9. IAM Compromise Containment

IAM compromise is one of the most critical cloud incident scenarios because attackers can rapidly escalate privileges and move laterally across cloud environments.

Common indicators of IAM compromise include:

- Impossible travel authentication
- MFA bypass attempts
- New access key creation
- Unauthorized role assumptions
- Excessive failed logins
- API activity from unusual locations
- Unexpected privilege escalation

Immediate response actions should focus on disabling attacker access while preserving evidence.

---

## 9.1 AWS IAM Containment

For AWS-related IAM incidents:

- Disable compromised IAM users
- Revoke STS tokens
- Delete unauthorized access keys
- Restrict AssumeRole trust policies
- Validate CloudTrail integrity
- Review GuardDuty findings

Investigators must also review all recently modified IAM policies and permissions boundaries.

---

## 9.2 Azure Identity Containment

For Azure and Entra ID incidents:

- Disable compromised accounts
- Revoke active sessions
- Force password reset
- Block sign-in
- Review Conditional Access changes
- Audit recent role assignments

Special attention should be given to Global Administrator activity.

---

## 9.3 GCP IAM Containment

For GCP incidents:

- Disable compromised identities
- Rotate service account keys
- Revoke OAuth tokens
- Audit IAM bindings
- Review organization-level permissions

Investigators should also validate whether workload identity federation was abused.

---

# 10. Cloud Workload Containment

Cloud workloads such as virtual machines, containers, and serverless functions may be used by attackers for persistence, lateral movement, malware deployment, or data exfiltration.

Containment strategies must therefore isolate affected systems without unnecessarily disrupting unrelated services.

---

## 10.1 Virtual Machine Isolation

Affected EC2 instances, Azure VMs, or GCE workloads should be isolated using cloud-native controls.

Recommended actions include:

- Removing internet-facing access
- Applying quarantine security groups
- Restricting outbound communication
- Suspending autoscaling replication
- Preserving workload snapshots
- Capturing volatile evidence where feasible

Systems should not be terminated before forensic snapshots are collected.

---

## 10.2 Kubernetes and Container Isolation

Containerized environments require additional containment controls because workloads are highly dynamic and interconnected.

Containment procedures may include:

- Isolating affected namespaces
- Cordoning compromised nodes
- Blocking pod-to-pod communication
- Removing malicious workloads
- Restricting service account permissions
- Capturing Kubernetes audit logs

Investigators must verify whether cluster-wide secrets were accessed.

---

## 10.3 Serverless Containment

Serverless functions may be abused for persistence or malicious automation.

Containment actions include:

- Disabling event triggers
- Removing execution permissions
- Restricting API gateway exposure
- Reviewing deployment history
- Capturing function configuration

Special attention should be given to newly modified functions.

---

# 11. Storage Exposure Containment

Cloud storage exposure incidents frequently result in regulatory reporting obligations and potential data breach investigations.

Common exposure scenarios include:

- Public S3 buckets
- Public Azure Blob containers
- Public GCS buckets
- Exposed database snapshots
- Weakly restricted object permissions

Containment activities must prioritize immediate access restriction while preserving evidence of exposure.

---

## 11.1 Immediate Actions

Responders should:

- Remove public permissions
- Restrict object access
- Preserve access logs
- Enable encryption validation
- Snapshot affected storage
- Review recent object downloads

If sensitive or regulated data is involved, the Legal and Compliance teams must be engaged immediately.

---

# 12. Data Exfiltration Containment

Cloud attackers often attempt to exfiltrate data using legitimate cloud APIs, making detection and containment difficult.

Indicators of cloud exfiltration include:

- Large outbound transfers
- Mass object downloads
- Excessive API read activity
- Geographic anomalies
- Unusual synchronization behavior

Containment procedures should focus on rapidly stopping outbound activity while preserving evidence.

---

## 12.1 Containment Actions

Recommended actions include:

- Blocking outbound traffic
- Restricting storage access
- Disabling compromised identities
- Enabling enhanced logging
- Preserving object access logs
- Increasing DLP monitoring

After containment, investigators must verify whether historical data access occurred prior to detection.

---

# 13. Cloud Malware and Cryptomining Containment

Cloud cryptomining attacks can rapidly increase operational costs and indicate broader compromise.

Common indicators include:

- Unexpected CPU spikes
- Excessive autoscaling
- Unknown containers or processes
- Outbound communication to mining pools
- Unauthorized scheduled tasks

Containment activities should isolate affected workloads while preserving forensic evidence.

---

## 13.1 Recommended Actions

Responders should:

- Isolate affected workloads
- Disable autoscaling replication
- Block known mining pool traffic
- Snapshot compromised systems
- Preserve runtime telemetry
- Audit startup scripts and cron jobs

Investigators must determine whether the attacker achieved persistence or privilege escalation.

---

# 14. Cross-Account Containment

Sophisticated cloud attackers frequently pivot across cloud accounts, subscriptions, or projects using trust relationships and federation.

Containment efforts must therefore include:

- Reviewing AssumeRole trust relationships
- Auditing federation settings
- Restricting shared credentials
- Validating management account integrity
- Reviewing CI/CD integration access

Cross-account compromise may significantly increase incident severity.

---

# 15. MSSP Multi-Tenant Containment

For MSSP-managed environments, containment procedures must ensure complete segregation between clients.

Containment teams must:

- Validate tenant isolation
- Restrict analyst visibility
- Prevent cross-client evidence exposure
- Maintain separate communication channels
- Follow contractual SLA notification timelines

Any incident affecting shared management infrastructure must be escalated immediately to executive management.

---

# 16. Regulatory and Legal Considerations

Cloud incidents may trigger legal, contractual, or regulatory reporting obligations.

Containment activities must support:

- RBI reporting requirements
- CERT-In reporting obligations
- ISO 27001 evidence preservation
- Legal hold procedures
- Client notification obligations

Responders must avoid modifying or deleting evidence without authorization.

---

# 17. Communication Requirements

Clear communication is critical during containment activities.

Internal stakeholders requiring notification include:

- SOC Lead
- Cloud Security Team
- Incident Response Team
- Management
- Legal and Compliance teams

External communication may include:

- Cloud providers
- Clients
- Regulators
- Third-party IR retainers

Only approved communication templates should be used.

Reference:
`05_ESCALATION-AND-COMMUNICATION/`

---

# 18. Containment Validation

Containment is not considered complete until validation activities confirm attacker activity has stopped.

Validation should confirm:

- Compromised identities are disabled
- Active sessions are revoked
- Public exposure is removed
- Malicious traffic is blocked
- Persistence mechanisms are removed
- Logging remains operational
- No continued exfiltration exists

Enhanced monitoring should remain active throughout the investigation lifecycle.

---

# 19. Transition to Eradication

Once containment is validated, the incident transitions into eradication and recovery activities.

Typical next steps include:

- Removing persistence mechanisms
- Rebuilding compromised workloads
- Rotating credentials
- Hardening IAM controls
- Applying security patches
- Restoring trusted configurations

Root cause analysis must begin immediately after stabilization.

---

# 20. Related Documents

| Document | Path |
|---|---|
| Cloud Master Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md` |
| Cloud L1 Triage | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md` |
| Cloud L2 Investigation | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md` |
| Cloud L3 Forensics | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L3-Forensics.md` |
| Cloud AWS Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-AWS-Specific.md` |
| Cloud Azure Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Azure-Specific.md` |
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