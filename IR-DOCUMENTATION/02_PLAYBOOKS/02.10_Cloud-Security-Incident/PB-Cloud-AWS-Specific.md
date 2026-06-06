# Playbook: AWS Cloud Security Incident Response Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Playbook – AWS Cloud Security Incident Response Procedures |
| Document ID | IR-PB-AWS-001 |
| Version | 1.0 |
| Effective Date | 21-May-2026 |
| Owner | SOC Manager / Cloud Security Lead / Incident Response Team |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 AWS security incident |

---

# 2. Purpose

This playbook defines standardized procedures for responding to AWS-specific security incidents affecting enterprise and MSSP-managed AWS environments.

AWS environments are highly dynamic and API-driven. Security incidents involving AWS infrastructure often evolve rapidly because attackers can leverage IAM abuse, automation pipelines, cloud-native services, and cross-account trust relationships to escalate privileges and expand their access.

This document provides detailed operational guidance for:

- AWS IAM compromise investigations
- EC2 compromise response
- S3 exposure incidents
- AWS persistence detection
- CloudTrail investigation
- GuardDuty alert handling
- Cross-account compromise response
- AWS network containment
- EKS and container investigations
- AWS forensic evidence preservation
- AWS-specific eradication and recovery procedures

This playbook supplements the master cloud security playbook and should be used during any AWS-related incident investigation.

---

# 3. Scope

## 3.1 In Scope

This playbook applies to AWS incidents involving:

- AWS IAM
- EC2 instances
- S3 buckets
- VPC networking
- Security Groups
- Lambda functions
- EKS clusters
- CloudTrail
- GuardDuty
- AWS Organizations
- Route53
- RDS
- CloudFormation
- AWS Secrets Manager
- AWS Systems Manager (SSM)
- AWS CodePipeline and DevOps tooling

---

## 3.2 Typical AWS Incident Types

| Incident Type | Description |
|---|---|
| IAM Compromise | Stolen access keys or session abuse |
| S3 Exposure | Public or misconfigured bucket access |
| EC2 Compromise | Malware or unauthorized access |
| Cryptomining | Unauthorized compute usage |
| Cross-Account Abuse | Malicious AssumeRole activity |
| Lambda Abuse | Malicious serverless execution |
| EKS Compromise | Kubernetes cluster compromise |
| CloudTrail Tampering | Logging disabled or modified |
| API Abuse | Unauthorized AWS API activity |
| Data Exfiltration | Unauthorized S3 or database access |

---

# 4. AWS Shared Responsibility Considerations

During AWS incident response, teams must clearly understand the AWS shared responsibility model.

AWS secures:

- Physical datacenters
- Hypervisor infrastructure
- Managed service availability
- Underlying hardware

The customer remains responsible for:

- IAM configuration
- S3 permissions
- EC2 security
- Security Groups
- Application security
- Logging configuration
- Encryption settings
- Patch management
- Data protection

Misunderstanding these responsibilities can lead to delayed containment and incomplete remediation.

---

# 5. AWS Incident Detection Sources

AWS incidents may be identified through multiple native and third-party detection sources.

---

## 5.1 Native AWS Detection Sources

| Service | Purpose |
|---|---|
| GuardDuty | Threat detection |
| CloudTrail | API activity logging |
| Security Hub | Aggregated security findings |
| AWS Config | Configuration monitoring |
| VPC Flow Logs | Network telemetry |
| CloudWatch | Monitoring and alerting |
| Macie | Sensitive data discovery |
| IAM Access Analyzer | External access identification |

---

## 5.2 Third-Party Detection Sources

Additional detection visibility may come from:

- SIEM platforms
- EDR telemetry
- CSPM tools
- Threat intelligence platforms
- DLP monitoring
- Kubernetes runtime security tools
- MSSP monitoring systems

---

# 6. AWS Investigation Priorities

AWS investigations should prioritize identity and API activity because most AWS attacks involve IAM abuse.

Investigators must immediately review:

- IAM users and roles
- Access key usage
- STS token activity
- CloudTrail logs
- Cross-account trust relationships
- Security Group modifications
- S3 bucket policy changes
- EC2 metadata access
- Newly created resources

The objective is to identify how the attacker gained access, what permissions were abused, and whether persistence mechanisms remain active.

---

# 7. AWS IAM Compromise Investigation

IAM compromise is one of the most severe AWS incident scenarios because attackers can rapidly gain administrative control over cloud infrastructure.

---

## 7.1 Common Indicators

Indicators of AWS IAM compromise include:

- Unusual API activity
- Impossible travel authentication
- Unauthorized key creation
- MFA deactivation
- Excessive AssumeRole activity
- New IAM users created unexpectedly
- Unauthorized policy modifications
- API activity from suspicious IP addresses

---

## 7.2 Investigation Steps

Investigators should:

- Review CloudTrail logs
- Identify affected IAM entities
- Review recently created access keys
- Validate MFA enforcement
- Review trust relationships
- Identify privilege escalation attempts
- Audit administrator activity
- Check AWS Organizations changes

---

## 7.3 Immediate Containment

Containment actions may include:

- Disabling IAM users
- Revoking STS sessions
- Removing malicious access keys
- Restricting AssumeRole permissions
- Blocking suspicious IP addresses
- Enabling enhanced monitoring

Before credential rotation, critical evidence should be preserved whenever operationally feasible.

---

# 8. EC2 Compromise Investigation

Compromised EC2 instances may be used for malware deployment, persistence, cryptomining, lateral movement, or data exfiltration.

Investigations should focus on determining:

- Initial access vector
- Attacker persistence
- Network communication
- Privilege escalation
- Data access activity
- Command execution history

---

## 8.1 Common Indicators

Indicators may include:

- Unusual outbound traffic
- High CPU utilization
- Unknown processes
- Unexpected user accounts
- Security Group changes
- Unauthorized software installation
- Suspicious cron jobs
- Communication with known malicious IPs

---

## 8.2 Containment Procedures

Recommended actions include:

- Isolating affected EC2 instances
- Applying quarantine Security Groups
- Restricting outbound communication
- Preserving EBS snapshots
- Capturing volatile evidence where possible
- Blocking malicious destinations

Systems should not be terminated before evidence preservation activities are completed.

---

# 9. S3 Exposure and Data Breach Investigation

S3 exposure incidents are among the most common AWS security events and frequently result in regulatory and legal implications.

---

## 9.1 Common Exposure Scenarios

| Scenario | Example |
|---|---|
| Public bucket access | Bucket exposed to internet |
| Misconfigured bucket policy | Excessive permissions |
| Anonymous object access | Public file exposure |
| Cross-account exposure | Unauthorized AWS account access |

---

## 9.2 Investigation Priorities

Investigators must determine:

- Whether sensitive data was exposed
- Whether unauthorized downloads occurred
- Which objects were accessed
- How long exposure existed
- Whether attacker persistence exists

Critical evidence sources include:

- S3 access logs
- CloudTrail object access events
- Bucket policies
- IAM permissions
- Macie findings

---

## 9.3 Immediate Containment

Containment activities include:

- Removing public access
- Restricting bucket policies
- Enabling encryption validation
- Preserving access logs
- Blocking external sharing

If regulated data is involved, Legal and Compliance teams must be engaged immediately.

---

# 10. AWS Persistence Mechanisms

Attackers frequently establish persistence within AWS environments to maintain long-term access.

Common AWS persistence techniques include:

- Rogue IAM users
- Hidden access keys
- AssumeRole abuse
- Lambda persistence
- Malicious CloudFormation templates
- Backdoor Security Groups
- Unauthorized federated identities
- Startup scripts in EC2 user-data

Investigators must audit all identity-related changes during the compromise window.

---

# 11. AWS CloudTrail Investigation

CloudTrail is one of the most critical evidence sources during AWS incident investigations.

CloudTrail analysis helps investigators determine:

- Who performed actions
- Which APIs were used
- Source IP addresses
- Resource modifications
- Timeline reconstruction
- Privilege escalation activity

---

## 11.1 Key CloudTrail Events

| Event Type | Importance |
|---|---|
| ConsoleLogin | Authentication activity |
| AssumeRole | Cross-account access |
| CreateAccessKey | Credential creation |
| PutBucketPolicy | S3 exposure |
| AuthorizeSecurityGroupIngress | Firewall modification |
| StopLogging | Logging tampering |
| CreateUser | Persistence creation |

---

## 11.2 Logging Integrity Checks

Investigators must verify:

- CloudTrail remained enabled
- Logs were not deleted
- Multi-region logging was active
- Log forwarding to SIEM succeeded

Tampering with CloudTrail significantly increases incident severity.

---

# 12. GuardDuty Investigation

GuardDuty provides AWS-native threat detection capabilities and often generates the first indicators of compromise.

Common GuardDuty findings include:

- Credential compromise
- API abuse
- Cryptomining activity
- Unauthorized access
- Malware communication
- Reconnaissance behavior

GuardDuty findings should always be correlated with CloudTrail activity and network telemetry.

---

# 13. EKS and Kubernetes Investigation

Compromise of Amazon EKS environments can lead to widespread cloud impact because attackers may gain access to containers, secrets, service accounts, and cloud APIs.

---

## 13.1 Investigation Focus Areas

Investigators should review:

- Kubernetes audit logs
- Service account permissions
- Cluster role bindings
- Container images
- Pod execution history
- Secrets access
- Network policies

---

## 13.2 Containment Actions

Containment may include:

- Isolating namespaces
- Cordoning nodes
- Removing malicious pods
- Restricting API server access
- Rotating Kubernetes secrets

Investigators must determine whether AWS IAM roles associated with Kubernetes workloads were abused.

---

# 14. AWS Network Containment

AWS network containment primarily relies on Security Groups, NACLs, and VPC segmentation.

Containment actions may include:

- Blocking malicious IPs
- Restricting inbound access
- Restricting outbound traffic
- Applying quarantine Security Groups
- Enabling enhanced VPC Flow Logs

Changes to Security Groups must be documented and approved through incident management procedures.

---

# 15. AWS Forensic Evidence Collection

AWS evidence collection must prioritize preservation of cloud-native telemetry before resources are modified or deleted.

---

## 15.1 Critical Evidence Sources

| Evidence Type | Examples |
|---|---|
| API logs | CloudTrail |
| Network telemetry | VPC Flow Logs |
| Storage access logs | S3 Access Logs |
| IAM evidence | Access keys and policies |
| Workload evidence | EBS snapshots |
| Runtime telemetry | EC2 process and memory data |

---

## 15.2 Evidence Preservation Requirements

Investigators must:

- Export logs securely
- Preserve EBS snapshots
- Hash exported evidence
- Record timestamps in UTC
- Maintain chain-of-custody documentation

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 16. AWS Eradication Guidance

After containment is validated, eradication activities should focus on removing attacker persistence and restoring trusted configurations.

Typical eradication actions include:

- Removing rogue IAM users
- Rotating credentials
- Rebuilding compromised EC2 instances
- Updating Security Groups
- Hardening S3 permissions
- Replacing compromised AMIs
- Patching vulnerable applications

All eradication actions must be documented.

---

# 17. AWS Recovery Guidance

Recovery activities should ensure systems are safely returned to production without reintroducing attacker access.

Recovery validation should confirm:

- Logging is operational
- IAM is hardened
- Persistence mechanisms removed
- Monitoring enabled
- Security baselines restored
- Sensitive data integrity validated

Enhanced monitoring should remain active following recovery.

---

# 18. MSSP AWS Considerations

For MSSP-managed AWS environments:

- Cross-account access must be reviewed carefully
- Shared tooling increases blast radius
- Client evidence segregation is mandatory
- Separate communication timelines may apply
- Tenant isolation must be validated

Any compromise affecting shared management infrastructure must be escalated immediately.

---

# 19. Regulatory and Compliance Considerations

AWS incidents involving sensitive data may trigger:

- RBI reporting obligations
- CERT-In reporting
- Client contractual notification requirements
- Data breach notification laws
- ISO 27001 audit requirements

Legal and Compliance teams must be engaged early during major incidents.

---

# 20. Related Documents

| Document | Path |
|---|---|
| Cloud Master Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md` |
| Cloud Containment Procedures | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Containment.md` |
| Cloud L1 Triage | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md` |
| Cloud L2 Investigation | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md` |
| Cloud L3 Forensics | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L3-Forensics.md` |
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
