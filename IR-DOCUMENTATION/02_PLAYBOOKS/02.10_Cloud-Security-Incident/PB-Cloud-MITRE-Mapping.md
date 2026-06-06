# Playbook: Cloud Security Incident – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Cloud Security Incident (MITRE ATT&CK Mapping)    |
| Document ID    | IR-PB-CLD-MITRE-001                                          |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | SOC Manager / Threat Detection Team / Incident Response Team |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 cloud security incident        |

---

## 2. Purpose

This document provides the MITRE ATT&CK framework mapping for cloud security incidents handled across enterprise and MSSP-managed environments. Cloud attacks represent a fundamentally different threat landscape compared to traditional on-premises intrusions because attackers operate against API-driven, identity-centric, and highly scalable infrastructure where a single compromised credential can lead to organization-wide compromise within minutes.

This mapping serves to:

- Align detected cloud attack behaviors to MITRE ATT&CK Enterprise and Cloud-specific techniques
- Improve analyst understanding of cloud attacker objectives across all attack stages
- Standardize threat hunting and investigation workflows for AWS, Azure, and GCP environments
- Improve detection engineering and SIEM/EDR/CSPM rule development for cloud threats
- Support L2/L3 scoping by identifying likely next-stage techniques after initial cloud access
- Provide audit-ready documentation for ISO 27001, NIST CSF, and RBI compliance requirements
- Enable structured threat hunting across observed cloud TTPs
- Support post-incident reporting at technical and executive levels
- Identify detection gaps specific to cloud attack vectors
- Support purple team exercises and tabletop scenarios

This document is a living reference. Analysts must use it during L2/L3 investigation phases and update it after major incidents when new cloud-specific techniques are observed.

---

## 3. Scope

### 3.1 In Scope

Applies to all cloud security incidents handled under:

- PB-Cloud-Master.md
- PB-Cloud-L1-Triage.md
- PB-Cloud-L2-Investigation.md
- PB-Cloud-L3-Forensics.md
- PB-Cloud-Containment.md
- PB-Cloud-AWS-Specific.md
- PB-Cloud-Azure-Specific.md
- PB-Cloud-GCP-Specific.md

Attack classes covered:

- Cloud IAM compromise and credential abuse
- Cloud API abuse and unauthorized operations
- Cloud storage exposure and data exfiltration
- Cloud workload compromise including EC2, Azure VM, and GCE
- Kubernetes and container environment attacks
- Serverless function abuse
- OAuth and federation trust exploitation
- CI/CD pipeline compromise in cloud environments
- Cross-account and cross-tenant compromise
- Cloud cryptomining and resource hijacking
- Cloud-native persistence mechanisms
- Cloud logging and monitoring evasion
- Multi-cloud lateral movement

---

### 3.2 Supported Cloud Platforms

| Platform | Coverage |
|---|---|
| AWS | IAM, EC2, S3, Lambda, EKS, CloudTrail, GuardDuty |
| Azure | Entra ID, Azure VM, AKS, Blob Storage, Sentinel |
| GCP | IAM, Compute Engine, GKE, GCS, SCC |
| Kubernetes | EKS, AKS, GKE, self-managed clusters |
| Containers | Docker and container runtime attacks |
| SaaS Integrations | OAuth, federation, and SSO abuse |
| CI/CD | Cloud Build, Azure DevOps, CodePipeline |

---

## 4. MITRE ATT&CK Framework Reference

| Field | Value |
|---|---|
| Framework | MITRE ATT&CK Enterprise |
| Version Referenced | v14 (verify current at attack.mitre.org) |
| Supplementary | MITRE ATT&CK for Containers and Cloud Platforms |
| Scope | Enterprise covering cloud, containers, identity, and CI/CD |

---

## 5. Cloud Attack Lifecycle Overview

Cloud attacks typically follow a structured lifecycle. Understanding this lifecycle helps analysts predict attacker behavior and identify techniques that may be occurring even when not yet detected.

The cloud attack lifecycle commonly follows:

1. Reconnaissance of cloud assets and exposed services
2. Initial access through credentials, exposed APIs, or misconfiguration
3. Execution using cloud-native services, workloads, or automation
4. Persistence through IAM manipulation, automation abuse, or backdoors
5. Privilege escalation using IAM policies, roles, and federation
6. Defense evasion through logging tampering and artifact removal
7. Credential access targeting secrets, tokens, and cloud metadata
8. Discovery of cloud resources, permissions, and sensitive data
9. Lateral movement across accounts, projects, and subscriptions
10. Collection targeting cloud storage, databases, and repositories
11. Exfiltration using cloud APIs, storage synchronization, and web services
12. Impact through ransomware, destruction, or resource hijacking

Each stage is mapped in detail in the sections below.

---

## 6. Cloud Attack – Full TTP Matrix

### 6.1 Reconnaissance

Reconnaissance activities are used by attackers to identify cloud assets, exposed services, IAM weaknesses, storage exposure, and publicly accessible infrastructure before launching an attack.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1595 | Active Scanning | T1595.001 Scanning IP Blocks | All | Automated scanning of cloud IP ranges for exposed services |
| T1595 | Active Scanning | T1595.002 Vulnerability Scanning | All | Scanning cloud services for known vulnerabilities |
| T1580 | Cloud Infrastructure Discovery | — | AWS / Azure / GCP | Enumerating cloud services, accounts, and resources |
| T1589 | Gather Victim Identity Information | T1589.001 Credentials | All | Searching for exposed cloud credentials in public sources |
| T1589 | Gather Victim Identity Information | T1589.002 Email Addresses | All | Gathering identity information for phishing against cloud admins |
| T1526 | Cloud Service Discovery | — | AWS / Azure / GCP | Enumerating available cloud services and APIs |
| T1613 | Container and Resource Discovery | — | Kubernetes / EKS / AKS / GKE | Identifying containers, pods, nodes, and cluster resources |
| T1596 | Search Open Technical Databases | T1596.005 Scan Databases | All | Searching Shodan, Censys for exposed cloud services |
| T1593 | Search Open Websites/Domains | T1593.002 Search Engines | All | Using search engines to identify exposed cloud resources |

---

### 6.2 Initial Access

Initial access in cloud environments most commonly occurs through identity compromise, exposed credentials, misconfigured services, or OAuth abuse. Unlike traditional environments, attackers often do not need to exploit vulnerabilities because misconfigured IAM permissions or exposed API keys provide direct access.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1078 | Valid Accounts | T1078.004 Cloud Accounts | AWS / Azure / GCP | Stolen or compromised cloud account credentials |
| T1078 | Valid Accounts | T1078.002 Domain Accounts | Azure / Entra ID | Domain accounts with cloud access abused |
| T1528 | Steal Application Access Token | — | All | OAuth tokens stolen from code, logs, or exposed applications |
| T1552 | Unsecured Credentials | T1552.001 Credentials in Files | All | API keys exposed in code repositories or config files |
| T1552 | Unsecured Credentials | T1552.005 Cloud Instance Metadata | AWS / Azure / GCP | IMDS metadata service abused for credential access |
| T1199 | Trusted Relationship | — | All | Compromising MSP or vendor with cloud access to target |
| T1566 | Phishing | T1566.002 Spearphishing Link | All | Phishing targeting cloud admins for credential harvest |
| T1190 | Exploit Public-Facing Application | — | All | Exploiting exposed cloud APIs or applications |
| T1133 | External Remote Services | — | AWS / Azure / GCP | Abusing legitimate remote access into cloud environments |

---

### 6.3 Execution

Cloud attackers execute malicious operations using cloud-native APIs, workload command execution, serverless functions, containers, and automation tools. Execution in cloud environments often leaves traces in API logs rather than traditional process telemetry.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1059 | Command and Scripting Interpreter | T1059.001 PowerShell | Azure / AWS | PowerShell used via VM access or cloud automation |
| T1059 | Command and Scripting Interpreter | T1059.004 Unix Shell | AWS / GCP | Bash execution on Linux cloud workloads |
| T1059 | Command and Scripting Interpreter | T1059.009 Cloud API | AWS / Azure / GCP | Cloud CLI and API used for malicious operations |
| T1648 | Serverless Execution | — | AWS Lambda / Azure Functions / GCP Functions | Malicious serverless function execution |
| T1610 | Deploy Container | — | EKS / AKS / GKE | Deploying unauthorized containers |
| T1609 | Container Administration Command | — | Kubernetes | Executing commands within containers |
| T1651 | Cloud Administration Command | — | AWS / Azure / GCP | Using cloud admin tools for malicious execution |
| T1072 | Software Deployment Tools | — | CI/CD | Abusing cloud deployment tools for execution |
| T1569 | System Services | T1569.002 Service Execution | AWS / Azure | Service creation and execution on cloud workloads |

---

### 6.4 Persistence

Cloud persistence differs significantly from traditional environments. Attackers commonly create hidden IAM entities, abuse automation, implant serverless functions, and establish OAuth grants to maintain long-term access that survives workload restarts and credential resets.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1098 | Account Manipulation | T1098.001 Additional Cloud Credentials | AWS / Azure / GCP | New access keys or credentials created for persistence |
| T1098 | Account Manipulation | T1098.003 Additional Cloud Roles | AWS / Azure / GCP | Elevated cloud roles added to compromised identity |
| T1136 | Create Account | T1136.003 Cloud Account | AWS / Azure / GCP | New cloud accounts created for persistent access |
| T1078 | Valid Accounts | T1078.004 Cloud Accounts | All | Maintaining access using legitimate cloud accounts |
| T1525 | Implant Internal Image | — | AWS / EKS / AKS / GKE | Malicious container image pushed to private registry |
| T1505 | Server Software Component | T1505.004 IIS Components | Azure | Persistence via server-side components |
| T1546 | Event Triggered Execution | T1546.003 WMI | Azure VM / AWS EC2 | WMI event subscription for persistence |
| T1053 | Scheduled Task/Job | T1053.005 Scheduled Task | Azure VM / EC2 | Scheduled task created for persistent execution |
| T1053 | Scheduled Task/Job | T1053.003 Cron | AWS / GCP Linux | Cron job created for persistence on Linux workloads |
| T1648 | Serverless Execution | — | Lambda / Azure Functions | Malicious functions deployed as persistence mechanism |

---

### 6.5 Privilege Escalation

Cloud privilege escalation frequently relies on IAM misconfigurations, excessive permissions, and federation abuse. Attackers exploit overly permissive roles, trust policies, and automation to gain administrative access across cloud environments.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1068 | Exploitation for Privilege Escalation | — | All | Exploiting misconfigured cloud services for escalation |
| T1484 | Domain or Tenant Policy Modification | T1484.001 Group Policy Modification | Azure | Group Policy modified for cloud escalation |
| T1484 | Domain or Tenant Policy Modification | T1484.002 Trust Modification | AWS / Azure / GCP | Cloud trust relationships modified for escalation |
| T1548 | Abuse Elevation Control Mechanism | T1548.005 Temporary Elevated Cloud Access | AWS / Azure / GCP | Temporary elevated permissions abused |
| T1098 | Account Manipulation | T1098.003 Additional Cloud Roles | AWS / Azure / GCP | Privileged roles added to attacker-controlled identities |
| T1611 | Escape to Host | — | Kubernetes / Containers | Container escape to access underlying cloud host |

---

### 6.6 Defense Evasion

Cloud attackers frequently attempt to disable logging, tamper with audit trails, and evade monitoring to extend their dwell time. Logging tampering is one of the most critical indicators of sophisticated cloud attacks.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1562 | Impair Defenses | T1562.001 Disable or Modify Tools | All | Disabling security monitoring tools |
| T1562 | Impair Defenses | T1562.008 Disable Cloud Logs | AWS / Azure / GCP | CloudTrail, Activity Logs, or GCP Audit Logs disabled |
| T1562 | Impair Defenses | T1562.007 Disable or Modify Cloud Firewall | AWS / Azure / GCP | Security Groups or Firewall rules weakened |
| T1070 | Indicator Removal | T1070.009 Clear Persistence | All | Removing persistence artifacts after objectives achieved |
| T1070 | Indicator Removal | T1070.004 File Deletion | EC2 / Azure VM / GCE | Removing malicious files from cloud workloads |
| T1027 | Obfuscated Files or Information | T1027.010 Command Obfuscation | All | Encoding cloud CLI commands to evade detection |
| T1578 | Modify Cloud Compute Infrastructure | T1578.001 Create Snapshot | AWS / Azure / GCP | Snapshots created to clone data stealthily |
| T1578 | Modify Cloud Compute Infrastructure | T1578.002 Create Cloud Instance | AWS / Azure / GCP | New instances created outside monitoring scope |
| T1578 | Modify Cloud Compute Infrastructure | T1578.005 Modify Cloud Compute Configurations | All | Modifying cloud configurations to evade detection |

---

### 6.7 Credential Access

Credential access is a primary attacker objective in cloud environments. API keys, OAuth tokens, service account credentials, and instance metadata provide extensive access to cloud infrastructure.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1552 | Unsecured Credentials | T1552.001 Credentials in Files | All | API keys in configuration files, scripts, or repositories |
| T1552 | Unsecured Credentials | T1552.005 Cloud Instance Metadata | AWS / Azure / GCP | IMDS metadata endpoint queried for credentials |
| T1552 | Unsecured Credentials | T1552.007 Container API | Kubernetes | Kubernetes API queried for secrets |
| T1528 | Steal Application Access Token | — | All | OAuth tokens stolen via code or compromised applications |
| T1539 | Steal Web Session Cookie | — | All | Session cookies stolen from web-accessible cloud services |
| T1606 | Forge Web Credentials | T1606.002 SAML Tokens | Azure / AWS | SAML tokens forged after identity infrastructure compromise |
| T1555 | Credentials from Password Stores | T1555.005 Password Managers | All | Cloud-stored password manager credentials accessed |
| T1003 | OS Credential Dumping | T1003.001 LSASS Memory | EC2 / Azure VM | LSASS dumped on compromised cloud workloads |

---

### 6.8 Discovery

Discovery activities allow attackers to enumerate cloud resources, understand organizational structure, identify high-value targets, and plan lateral movement paths.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1580 | Cloud Infrastructure Discovery | — | AWS / Azure / GCP | Enumerating cloud accounts, regions, and resources |
| T1526 | Cloud Service Discovery | — | All | Identifying available cloud services and enabled APIs |
| T1087 | Account Discovery | T1087.004 Cloud Account | AWS / Azure / GCP | Enumerating cloud users, roles, and service accounts |
| T1613 | Container and Resource Discovery | — | Kubernetes | Enumerating pods, namespaces, nodes, and secrets |
| T1082 | System Information Discovery | — | EC2 / Azure VM / GCE | OS and system profiling on cloud workloads |
| T1083 | File and Directory Discovery | — | EC2 / Azure VM / GCE | File system enumeration on cloud workloads |
| T1046 | Network Service Discovery | — | All | Internal cloud network scanning for lateral movement |
| T1018 | Remote System Discovery | — | All | Identifying other systems in cloud environment |
| T1069 | Permission Groups Discovery | T1069.003 Cloud Groups | AWS / Azure / GCP | Enumerating IAM groups and role memberships |
| T1530 | Data from Cloud Storage | — | S3 / Blob / GCS | Discovering storage contents during reconnaissance |

---

### 6.9 Lateral Movement

Cloud lateral movement relies heavily on trust relationships, federation, shared credentials, and cloud-native automation. Attackers frequently pivot across cloud accounts, subscriptions, and projects using legitimate cloud mechanisms.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1021 | Remote Services | T1021.007 Cloud Services | AWS / Azure / GCP | Cloud services abused for lateral movement |
| T1021 | Remote Services | T1021.004 SSH | EC2 / GCE / Azure VM | SSH lateral movement with harvested credentials |
| T1021 | Remote Services | T1021.001 RDP | Azure VM / EC2 | RDP lateral movement on cloud workloads |
| T1550 | Use Alternate Authentication Material | T1550.001 Application Access Token | All | OAuth and application tokens used for lateral movement |
| T1550 | Use Alternate Authentication Material | T1550.004 Web Session Cookie | All | Session cookies used to access additional cloud resources |
| T1548 | Abuse Elevation Control Mechanism | T1548.005 Temporary Elevated Cloud Access | AWS | Cross-account role assumption for lateral movement |
| T1610 | Deploy Container | — | Kubernetes | Deploying containers in new namespaces for lateral movement |
| T1534 | Internal Spearphishing | — | All | Internal communication used to spread within cloud org |

---

### 6.10 Collection

Cloud environments provide attackers with extensive collection opportunities because data is centralized in object storage, databases, code repositories, and secret management services.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1530 | Data from Cloud Storage | — | S3 / Azure Blob / GCS | Object storage data accessed and collected |
| T1213 | Data from Information Repositories | T1213.003 Code Repositories | All / CI/CD | Source code and secrets accessed from code repositories |
| T1005 | Data from Local System | — | EC2 / Azure VM / GCE | Files collected from cloud workload filesystems |
| T1119 | Automated Collection | — | All | Automated bulk data collection by malicious scripts |
| T1074 | Data Staged | T1074.002 Remote Data Staging | All | Data staged in cloud storage before exfiltration |
| T1560 | Archive Collected Data | T1560.001 Archive via Utility | All | Data compressed before exfiltration |
| T1602 | Data from Configuration Repository | T1602.001 SNMP MIB Dump | Network devices | Network configuration data collected |
| T1039 | Data from Network Shared Drive | — | EC2 / Azure VM | Data collected from network shares in cloud environment |

---

### 6.11 Command and Control

Cloud attackers establish C2 channels that blend with legitimate cloud traffic, making detection challenging. HTTPS-based C2, DNS tunneling, and abuse of legitimate cloud services are common approaches.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1071 | Application Layer Protocol | T1071.001 Web Protocols HTTPS | All | C2 over HTTPS blending with legitimate cloud traffic |
| T1071 | Application Layer Protocol | T1071.004 DNS | All | DNS-based C2 from compromised cloud workloads |
| T1572 | Protocol Tunneling | — | All | Tunneling C2 over legitimate protocols |
| T1573 | Encrypted Channel | T1573.002 Asymmetric Cryptography | All | Encrypted C2 using asymmetric cryptography |
| T1090 | Proxy | T1090.004 Domain Fronting | All | Domain fronting using CDNs for C2 obfuscation |
| T1102 | Web Service | T1102.002 Bidirectional Communication | All | Legitimate cloud services used as C2 channels |
| T1568 | Dynamic Resolution | T1568.002 Domain Generation Algorithms | All | DGA used for C2 domain rotation |
| T1008 | Fallback Channels | — | All | Multiple C2 channels for resilience |
| T1219 | Remote Access Software | — | All | Legitimate cloud RMM tools abused for C2 |

---

### 6.12 Exfiltration

Cloud environments provide multiple exfiltration paths including API-based data transfer, storage synchronization, and abuse of legitimate cloud services. Large-scale exfiltration is possible rapidly due to cloud bandwidth.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1537 | Transfer Data to Cloud Account | — | AWS / Azure / GCP | Data transferred to attacker-controlled cloud accounts |
| T1567 | Exfiltration Over Web Service | T1567.002 Exfiltration to Cloud Storage | All | Data exfiltrated to attacker cloud storage |
| T1041 | Exfiltration Over C2 Channel | — | All | Data exfiltrated through established C2 channel |
| T1048 | Exfiltration Over Alternative Protocol | T1048.003 Exfil Over Unencrypted Protocol | All | Data exfiltrated via non-standard protocol |
| T1020 | Automated Exfiltration | — | All | Automated bulk exfiltration by malicious scripts |
| T1030 | Data Transfer Size Limits | — | All | Data exfiltrated in small chunks to avoid detection |
| T1029 | Scheduled Transfer | — | All | Data exfiltrated on schedule to blend with traffic |

---

### 6.13 Impact

Cloud impact activities include ransomware deployment, data destruction, resource hijacking for cryptomining, and service disruption. Cloud environments amplify impact because resources can be scaled rapidly.

| Technique ID | Technique Name | Sub-Technique | Cloud Platform | Description |
|---|---|---|---|---|
| T1486 | Data Encrypted for Impact | — | All | Ransomware deployed across cloud workloads |
| T1485 | Data Destruction | — | All | Cloud data and snapshots deleted |
| T1496 | Resource Hijacking | — | All | Cloud compute hijacked for cryptomining |
| T1499 | Endpoint Denial of Service | T1499.002 Service Exhaustion Flood | All | Cloud services disrupted |
| T1490 | Inhibit System Recovery | — | All | Snapshots and backups deleted to prevent recovery |
| T1565 | Data Manipulation | T1565.001 Stored Data Manipulation | All | Cloud data integrity compromised |
| T1491 | Defacement | T1491.002 External Defacement | All | Publicly accessible cloud services defaced |

---

## 7. Kubernetes and Container Specific ATT&CK Mapping

Container and Kubernetes environments have specific attack techniques that extend the standard ATT&CK framework. These techniques apply to EKS, AKS, GKE, and self-managed Kubernetes clusters.

| Technique ID | Technique Name | Sub-Technique | Description |
|---|---|---|---|
| T1610 | Deploy Container | — | Deploying malicious containers in cluster |
| T1609 | Container Administration Command | — | Executing commands within existing containers |
| T1611 | Escape to Host | — | Breaking out of container to access underlying node |
| T1613 | Container and Resource Discovery | — | Enumerating cluster resources, pods, secrets |
| T1525 | Implant Internal Image | — | Pushing malicious images to private registries |
| T1552 | Unsecured Credentials | T1552.007 Container API | Accessing Kubernetes API for credentials |
| T1098 | Account Manipulation | T1098.003 Additional Cloud Roles | Kubernetes RBAC manipulation |
| T1053 | Scheduled Task/Job | T1053.007 Container Orchestration Job | CronJob abuse in Kubernetes |

---

## 8. Cloud IAM Attack Technique Deep Dive

IAM attacks represent the most common and highest-impact cloud attack vector. Understanding the specific techniques used to abuse cloud identity systems is critical for effective detection and response.

---

### 8.1 AWS IAM-Specific Techniques

| Attack Scenario | MITRE Technique | Sub-Technique | Description |
|---|---|---|---|
| Access key exposure | T1552 | T1552.001 Credentials in Files | AWS access keys exposed in code or config |
| Assume role abuse | T1548 | T1548.005 Temporary Elevated Cloud Access | Malicious AssumeRole for privilege escalation |
| New access key creation | T1098 | T1098.001 Additional Cloud Credentials | Persistent access through new IAM keys |
| New IAM user creation | T1136 | T1136.003 Cloud Account | Rogue IAM user for persistence |
| Policy attachment | T1098 | T1098.003 Additional Cloud Roles | Admin policy attached to attacker identity |
| Metadata service abuse | T1552 | T1552.005 Cloud Instance Metadata | IMDS v1 abused for credential theft |

---

### 8.2 Azure Entra ID-Specific Techniques

| Attack Scenario | MITRE Technique | Sub-Technique | Description |
|---|---|---|---|
| OAuth consent phishing | T1528 | — | Malicious app requesting excessive OAuth permissions |
| SAML token forgery | T1606 | T1606.002 SAML Tokens | Golden SAML attack |
| Refresh token theft | T1528 | — | Persistent OAuth tokens stolen |
| Role assignment abuse | T1098 | T1098.003 Additional Cloud Roles | Unauthorized Entra ID role assignment |
| Conditional Access bypass | T1562 | T1562.001 Disable or Modify Tools | Conditional Access policy weakened |
| Service principal abuse | T1098 | T1098.001 Additional Cloud Credentials | Malicious service principal for persistence |

---

### 8.3 GCP IAM-Specific Techniques

| Attack Scenario | MITRE Technique | Sub-Technique | Description |
|---|---|---|---|
| Service account key abuse | T1552 | T1552.001 Credentials in Files | Exposed service account keys abused |
| Workload identity abuse | T1548 | T1548.005 Temporary Elevated Cloud Access | Workload identity federation exploitation |
| Organization policy bypass | T1484 | T1484.002 Trust Modification | Org-level policies weakened |
| New service account creation | T1136 | T1136.003 Cloud Account | New service account for persistence |
| IAM binding modification | T1098 | T1098.003 Additional Cloud Roles | IAM policy bindings modified |
| API enablement | T1526 | — | Sensitive APIs enabled for attacker use |

---

## 9. Attack Chain Mapping by Cloud Scenario

### 9.1 AWS IAM Compromise Full Attack Chain

| Stage | Technique ID | Technique Name |
|---|---|---|
| Initial Access | T1552.001 | Unsecured Credentials: Credentials in Files |
| Initial Access | T1078.004 | Valid Accounts: Cloud Accounts |
| Execution | T1059.009 | Command and Scripting: Cloud API |
| Persistence | T1098.001 | Additional Cloud Credentials new access keys |
| Persistence | T1136.003 | Create Account: Cloud Account |
| Privilege Escalation | T1548.005 | Temporary Elevated Cloud Access AssumeRole |
| Defense Evasion | T1562.008 | Disable Cloud Logs CloudTrail disabled |
| Credential Access | T1552.005 | Cloud Instance Metadata IMDS abuse |
| Discovery | T1580 | Cloud Infrastructure Discovery |
| Discovery | T1526 | Cloud Service Discovery |
| Lateral Movement | T1548.005 | Cross-account role assumption |
| Collection | T1530 | Data from Cloud Storage S3 |
| Exfiltration | T1537 | Transfer Data to Cloud Account |
| Impact | T1496 | Resource Hijacking cryptomining |

---

### 9.2 Azure Identity Compromise Full Attack Chain

| Stage | Technique ID | Technique Name |
|---|---|---|
| Initial Access | T1528 | Steal Application Access Token OAuth |
| Initial Access | T1566.002 | Phishing: Spearphishing Link |
| Execution | T1059.001 | Command and Scripting: PowerShell |
| Persistence | T1098.001 | Account Manipulation: Additional Cloud Credentials |
| Privilege Escalation | T1098.003 | Additional Cloud Roles Global Admin |
| Defense Evasion | T1562.008 | Disable Cloud Logs Activity Logs |
| Defense Evasion | T1562.007 | Disable or Modify Cloud Firewall NSG |
| Credential Access | T1606.002 | Forge Web Credentials: SAML Tokens |
| Discovery | T1087.004 | Account Discovery: Cloud Account |
| Lateral Movement | T1550.001 | Use Alternate Authentication Material |
| Collection | T1530 | Data from Cloud Storage Blob |
| Exfiltration | T1567.002 | Exfiltration to Cloud Storage |
| Impact | T1486 | Data Encrypted for Impact Ransomware |

---

### 9.3 GCP Service Account Compromise Full Attack Chain

| Stage | Technique ID | Technique Name |
|---|---|---|
| Initial Access | T1552.001 | Unsecured Credentials in Files service account key |
| Execution | T1059.009 | Command and Scripting: Cloud API GCP CLI |
| Persistence | T1136.003 | Create Account: Cloud Account new service account |
| Privilege Escalation | T1548.005 | Temporary Elevated Cloud Access |
| Defense Evasion | T1562.008 | Disable Cloud Logs GCP Audit Logs |
| Credential Access | T1552.005 | Cloud Instance Metadata GCP metadata API |
| Discovery | T1580 | Cloud Infrastructure Discovery projects |
| Discovery | T1526 | Cloud Service Discovery APIs |
| Lateral Movement | T1021.007 | Remote Services Cloud Services |
| Collection | T1530 | Data from Cloud Storage GCS |
| Exfiltration | T1537 | Transfer Data to Cloud Account |
| Impact | T1485 | Data Destruction bucket deletion |

---

### 9.4 Kubernetes Cluster Compromise Full Attack Chain

| Stage | Technique ID | Technique Name |
|---|---|---|
| Initial Access | T1190 | Exploit Public-Facing Application exposed API |
| Initial Access | T1552.007 | Unsecured Credentials: Container API |
| Execution | T1609 | Container Administration Command kubectl exec |
| Execution | T1610 | Deploy Container malicious pod |
| Persistence | T1525 | Implant Internal Image malicious registry image |
| Persistence | T1053.007 | Scheduled Task/Job: Container Orchestration Job |
| Privilege Escalation | T1611 | Escape to Host container breakout |
| Defense Evasion | T1562.001 | Disable or Modify Tools runtime security |
| Credential Access | T1552.007 | Unsecured Credentials: Container API secrets |
| Discovery | T1613 | Container and Resource Discovery |
| Lateral Movement | T1021.007 | Remote Services Cloud Services |
| Collection | T1530 | Data from Cloud Storage persistent volumes |
| Exfiltration | T1041 | Exfiltration Over C2 Channel |
| Impact | T1496 | Resource Hijacking cryptomining |

---

### 9.5 Cloud Storage Exposure and Exfiltration Attack Chain

| Stage | Technique ID | Technique Name |
|---|---|---|
| Reconnaissance | T1580 | Cloud Infrastructure Discovery public buckets |
| Initial Access | T1190 | Exploit Public-Facing Application misconfigured storage |
| Discovery | T1530 | Data from Cloud Storage object enumeration |
| Collection | T1119 | Automated Collection bulk download |
| Collection | T1074.002 | Data Staged: Remote Data Staging |
| Exfiltration | T1537 | Transfer Data to Cloud Account |
| Exfiltration | T1567.002 | Exfiltration to Cloud Storage |

---

### 9.6 Cloud CI/CD Pipeline Compromise Attack Chain

| Stage | Technique ID | Technique Name |
|---|---|---|
| Initial Access | T1195.002 | Supply Chain Compromise: Software Supply Chain |
| Execution | T1072 | Software Deployment Tools CI/CD |
| Persistence | T1053.005 | Scheduled Task automated build trigger |
| Defense Evasion | T1562.008 | Disable Cloud Logs build audit disabled |
| Credential Access | T1552.001 | Unsecured Credentials CI/CD secrets |
| Collection | T1213.003 | Data from Code Repositories |
| Exfiltration | T1041 | Exfiltration Over C2 Channel |
| Impact | T1565.001 | Stored Data Manipulation code integrity |

---

### 9.7 Cloud Cryptomining Attack Chain

| Stage | Technique ID | Technique Name |
|---|---|---|
| Initial Access | T1078.004 | Valid Accounts: Cloud Accounts stolen credentials |
| Execution | T1059.009 | Command and Scripting: Cloud API |
| Execution | T1610 | Deploy Container mining container |
| Persistence | T1098.001 | Account Manipulation: Additional Cloud Credentials |
| Defense Evasion | T1578.002 | Create Cloud Instance outside monitored regions |
| Defense Evasion | T1562.008 | Disable Cloud Logs billing alerts disabled |
| Discovery | T1580 | Cloud Infrastructure Discovery compute resources |
| Impact | T1496 | Resource Hijacking cryptomining compute |

---

## 10. Detection Coverage Map

| Technique ID | Technique Name | Primary Detection Source | Secondary Source | Tool Stack |
|---|---|---|---|---|
| T1078.004 | Valid Accounts: Cloud | Identity threat detection | SIEM authentication logs | SIEM + Identity Protection |
| T1552.001 | Credentials in Files | Secret scanning tools | SIEM code push monitoring | DevSecOps + SIEM |
| T1552.005 | Cloud Instance Metadata | IMDS access monitoring | Host-based monitoring | EDR + SIEM |
| T1528 | Steal Application Access Token | OAuth activity monitoring | Identity logs | SIEM + IAM |
| T1580 | Cloud Infrastructure Discovery | Cloud audit anomalies | SIEM correlation | Cloud + SIEM |
| T1526 | Cloud Service Discovery | API enumeration alerts | GuardDuty / SCC / Defender | CSPM + SIEM |
| T1562.008 | Disable Cloud Logs | CloudTrail / Logging status | SIEM heartbeat | SIEM + Cloud Native |
| T1098.001 | Additional Cloud Credentials | IAM key creation alerts | Cloud audit logs | Cloud + SIEM |
| T1136.003 | Create Account: Cloud | New account creation alerts | IAM audit logs | Cloud + SIEM |
| T1548.005 | Temporary Elevated Cloud Access | AssumeRole monitoring | Cross-account auth alerts | SIEM + Cloud |
| T1537 | Transfer Data to Cloud Account | Egress monitoring | DLP alerts | Proxy + DLP |
| T1567.002 | Exfiltration to Cloud Storage | Proxy cloud upload monitoring | CASB alerts | Proxy + CASB |
| T1610 | Deploy Container | Kubernetes audit logs | Runtime monitoring | K8s Runtime + SIEM |
| T1611 | Escape to Host | Container runtime security | Host-based EDR | EDR + Runtime |
| T1613 | Container Discovery | Kubernetes audit logs | SIEM correlation | SIEM + K8s |
| T1496 | Resource Hijacking | Cloud billing anomalies | High CPU monitoring | CloudWatch + SIEM |
| T1486 | Data Encrypted for Impact | Ransomware behavior detection | Mass file modification | EDR + SIEM |
| T1485 | Data Destruction | Snapshot deletion alerts | Storage monitoring | Cloud + SIEM |
| T1578.002 | Create Cloud Instance | Unauthorized instance creation | Billing monitoring | Cloud + SIEM |
| T1562.007 | Disable Cloud Firewall | Security Group modification | NSG / Firewall audit | Cloud + SIEM |
| T1606.002 | Forge Web Credentials SAML | SAML token anomaly detection | Identity Protection | SIEM + IdP |
| T1071.001 | Web Protocols C2 | Proxy traffic analysis | DNS monitoring | Proxy + SIEM |
| T1059.009 | Cloud API Abuse | Cloud audit anomalies | Rate limiting alerts | Cloud + SIEM |

---

## 11. Threat Hunting Queries Reference

### 11.1 T1562.008 – Cloud Logging Disabled Detection

**Objective:** Detect when cloud audit logging is disabled by any identity.

**AWS CloudTrail Logic:**
- source: CloudTrail
- event_name: StopLogging
- event_source: cloudtrail.amazonaws.com
- user_identity: ANY
- timeframe: real-time alert

Pivot on:
- Identity that performed StopLogging action
- All API calls made by that identity in the prior 24 hours
- Whether CloudTrail was re-enabled after disablement

---

### 11.2 T1098.001 – New Cloud Access Key Creation

**Objective:** Detect unauthorized IAM access key creation.

**AWS CloudTrail Logic:**
- source: CloudTrail
- event_name: CreateAccessKey
- event_source: iam.amazonaws.com
- user_identity: NOT IN approved_admin_list
- timeframe: real-time alert

Pivot on:
- Identity that created the key
- Target user the key was created for
- All subsequent API calls using new access key

---

### 11.3 T1548.005 – Cross-Account Role Assumption Anomaly

**Objective:** Detect unusual AssumeRole activity across accounts.

**AWS CloudTrail Logic:**
- source: CloudTrail
- event_name: AssumeRole
- event_source: sts.amazonaws.com
- assumed_role_arn: NOT IN approved_cross_account_roles
- source_ip: NOT IN known_organizational_ip_ranges
- timeframe: real-time alert

Pivot on:
- Source identity and account
- Target role and destination account
- All API operations performed after successful assumption

---

### 11.4 T1552.005 – Cloud Instance Metadata Service Abuse

**Objective:** Detect abuse of cloud instance metadata API for credential theft.

**Logic:**
- source: EDR OR host-based monitoring
- event_type: network_connection OR http_request
- destination_ip: 169.254.169.254 OR equivalent metadata endpoint
- process_name: NOT IN known_metadata_access_processes
- timeframe: continuous monitoring

Pivot on:
- Process making metadata request
- Whether credentials were subsequently used from external IP
- Process parent chain

---

### 11.5 T1580 – Cloud Infrastructure Discovery Anomaly

**Objective:** Detect excessive cloud resource enumeration activity.

**Logic:**
- source: CloudTrail OR Azure Activity Logs OR GCP Audit Logs
- event_name: List* OR Describe* OR Get*
- count: greater than baseline_api_call_threshold_per_hour
- user_identity: ANY
- timeframe: last 1 hour rolling window

Pivot on:
- Identity performing excessive enumeration
- Resources being enumerated
- Whether enumeration preceded other suspicious activity

---

### 11.6 T1610 – Unauthorized Container Deployment

**Objective:** Detect deployment of unauthorized containers in Kubernetes clusters.

**Logic:**
- source: Kubernetes audit logs
- event_action: create
- resource_kind: Pod OR Deployment
- namespace: NOT IN approved_namespace_list OR image NOT IN approved_image_registry
- user_agent: NOT IN known_deployment_tools
- timeframe: real-time alert

Pivot on:
- Container image source and hash
- Namespace and service account used
- Network connections from new container

---

### 11.7 T1537 – Data Transfer to External Cloud Account

**Objective:** Detect data being transferred to attacker-controlled cloud storage.

**Logic:**
- source: proxy OR cloud audit logs
- event_type: cloud_storage_upload OR s3_put_object OR blob_upload
- destination_account: NOT IN approved_cloud_account_list
- bytes_transferred: greater than baseline_threshold
- timeframe: last 24 hours

Pivot on:
- Identity performing transfer
- Volume of data transferred
- Destination account ownership

---

### 11.8 T1496 – Cryptomining Resource Hijacking Detection

**Objective:** Detect unauthorized compute resources being used for cryptomining.

**Logic:**
- source: CloudWatch OR Azure Monitor OR GCP Monitoring
- metric: CPU_utilization
- value: greater than 80 percent sustained for 30 minutes
- instance_type: NOT IN known_high_compute_workloads
- network: outbound connections to known mining pool IP ranges

Pivot on:
- Instance creation time and identity
- Outbound network connections
- Processes running on instance

---

### 11.9 T1528 – OAuth Token Theft Detection

**Objective:** Detect OAuth token abuse from unusual locations.

**Logic:**
- source: Entra ID Sign-In Logs OR GCP OAuth Logs
- event_type: token_issuance
- source_ip: NOT IN known_organization_ip_ranges
- token_type: refresh_token OR access_token
- application: IN sensitive_application_list

Pivot on:
- IP address and geographic location
- Token usage patterns after issuance
- Applications accessed with stolen token

---

### 11.10 T1611 – Container Escape to Host Detection

**Objective:** Detect container breakout activity targeting the underlying cloud host.

**Logic:**
- source: container runtime security tool OR EDR
- event_type: privileged_container_exec OR host_namespace_access
- container_id: ANY
- parent_process: container_runtime_process
- child_process_namespace: host_namespace

Pivot on:
- Container image and registry
- Process execution chain
- Subsequent host-level activity

---

## 12. ATT&CK Navigator Layer Reference

The following technique IDs should be highlighted in an ATT&CK Navigator layer for cloud incidents:

| Tactic | Technique IDs to Highlight |
|---|---|
| Reconnaissance | T1595, T1580, T1589, T1526, T1613, T1596, T1593 |
| Initial Access | T1078.004, T1528, T1552.001, T1552.005, T1199, T1566.002, T1190 |
| Execution | T1059.001, T1059.004, T1059.009, T1648, T1610, T1609, T1651, T1072 |
| Persistence | T1098.001, T1098.003, T1136.003, T1078.004, T1525, T1546, T1053.005, T1648 |
| Privilege Escalation | T1068, T1484.002, T1548.005, T1098.003, T1611 |
| Defense Evasion | T1562.001, T1562.008, T1562.007, T1070.004, T1027.010, T1578.001, T1578.002 |
| Credential Access | T1552.001, T1552.005, T1552.007, T1528, T1539, T1606.002, T1003.001 |
| Discovery | T1580, T1526, T1087.004, T1613, T1082, T1083, T1046, T1069.003, T1530 |
| Lateral Movement | T1021.007, T1021.004, T1550.001, T1550.004, T1548.005, T1610 |
| Collection | T1530, T1213.003, T1005, T1119, T1074.002, T1560.001, T1039 |
| Command and Control | T1071.001, T1071.004, T1572, T1573.002, T1090.004, T1102.002, T1568.002 |
| Exfiltration | T1537, T1567.002, T1041, T1048, T1020, T1030, T1029 |
| Impact | T1486, T1485, T1496, T1499, T1490, T1565.001, T1491.002 |

---

## 13. Analyst Quick Lookup Table

Use this table for fast technique identification during active cloud incident investigations:

| If You Observe This… | MITRE Technique | Priority Action |
|---|---|---|
| CloudTrail StopLogging event detected | T1562.008 | Re-enable logging immediately; escalate to IR Team; review all prior API calls |
| New IAM access key created by unknown identity | T1098.001 | Disable key immediately; audit all actions taken with key |
| AssumeRole from unknown external account | T1548.005 | Remove trust relationship; escalate to IR Team |
| Vendor software process querying metadata endpoint | T1552.005 | Isolate workload; rotate instance credentials; escalate |
| Hundreds of Describe and List API calls in short window | T1580 | Investigate identity; check for subsequent exploitation |
| New cloud user account created outside approved process | T1136.003 | Disable account; audit actions; escalate |
| Malicious container deployed in production namespace | T1610 | Isolate namespace; remove container; escalate to L3 |
| High CPU on instance with unknown processes | T1496 | Isolate instance; block mining pool IPs; escalate |
| SAML token anomaly from unusual location | T1606.002 | Revoke token; reset identity; escalate |
| Large outbound transfer to unknown cloud account | T1537 | Block egress; escalate; activate data breach playbook |
| S3 bucket made public unexpectedly | T1190 | Restrict access; preserve logs; engage Legal/Compliance |
| Container privileged access to host namespace | T1611 | Isolate node; remove container; escalate immediately |
| GCP service account key created in unusual region | T1098.001 | Revoke key; audit actions; escalate |
| OAuth application granted excessive permissions | T1528 | Revoke consent; review accessed resources; escalate |
| Cross-account data replication to unknown account | T1537 | Stop replication; escalate; preserve evidence |
| Security Group modified to allow 0.0.0.0/0 inbound | T1562.007 | Revert rule; investigate identity; escalate |
| Kubernetes secrets accessed by unexpected service account | T1552.007 | Rotate secrets; audit RBAC; escalate |
| Lambda function modified with new execution permissions | T1648 | Revert function; audit trigger; escalate |
| Azure Conditional Access policy weakened or disabled | T1562.001 | Restore policy; investigate identity; escalate |

---

## 14. Cloud-Specific Detection Gaps and Recommendations

Cloud attacks exploit cloud-native features that many standard detection controls are not designed to monitor. The following gaps are commonly observed in enterprise cloud monitoring programs:

| Detection Gap | Why It Exists | Recommended Improvement |
|---|---|---|
| IMDS v1 not blocked allowing credential theft | Backward compatibility maintained | Enforce IMDS v2 across all EC2 instances and GCP equivalents |
| CloudTrail not enabled in all regions | Default configuration only enables single-region | Enable multi-region CloudTrail with log file validation |
| No alert on IAM key creation | IAM events not tuned for alerting | Implement real-time alert on CreateAccessKey |
| Cloud metadata API access not baselined | Metadata access treated as normal | Establish process whitelist for legitimate metadata access |
| No SBOM for cloud applications | Cloud workloads not tracked at dependency level | Implement SBOM generation for cloud deployments |
| Kubernetes audit logs not forwarded to SIEM | Cluster logging not configured | Enable and forward K8s audit logs to centralized SIEM |
| OAuth grants not reviewed regularly | OAuth consent not monitored | Implement periodic OAuth application review process |
| Cross-account access not monitored | Trusted accounts treated as safe | Apply same monitoring to cross-account activity as external |
| Cloud billing anomaly alerts not configured | Cost monitoring separate from security | Integrate billing anomaly detection into security monitoring |
| Container image signing not enforced | CI/CD pipelines allow unsigned images | Implement container image signing and admission control |
| GCP workload identity federation not audited | Federation treated as trusted | Monitor all workload identity token requests |
| Azure PIM not used for privileged roles | Standing privileged access maintained | Implement just-in-time privileged access management |

---

## 15. Post-Incident MITRE Mapping Update Requirements

After every P1/P2 cloud security incident, the L3 analyst or IR Team must complete the following:

| Action | Owner | Target |
|---|---|---|
| Review observed techniques against this mapping | L3 / IR Lead | Within 5 days of incident close |
| Add newly observed techniques not covered in document | L3 / IR Lead | Update this document |
| Update hunting queries with patterns from incident | L3 / Detection | Detection-Improvement-Log.md |
| Update ATT&CK Navigator layer with confirmed techniques | L3 / Detection | Internal TI platform |
| Add new IoCs to IoC output register | L3 / TI Team | IoC-Output-Register.md |
| Share TTP intelligence with TI team for threat profiling | L3 / TI | TTP-Intelligence-Report.md |

Reference: `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

Reference: `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`

---

## 16. Regulatory and Compliance Context

This MITRE mapping supports compliance with the following frameworks:

| Framework | Requirement | How This Mapping Helps |
|---|---|---|
| NIST CSF 2.0 | DE.AE, RS.AN, RS.MI | Structured detection, analysis, and response framework |
| NIST SP 800-53 | IR-4, IR-5, IR-8 | Technique-based incident handling and documentation |
| ISO 27001:2022 | A.5.24 through A.5.28 | Structured incident classification and IoC output |
| RBI Cyber Security Framework | Threat intelligence and IR capability | TTP-based hunting and enrichment for BFSI sector |
| NIST SP 800-161 | Supply Chain Risk Management | Cloud supply chain TTP coverage |

---

## 17. Related Documents

| Document | Path |
|---|---|
| Cloud Master Playbook | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md` |
| Cloud Containment Procedures | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Containment.md` |
| Cloud L1 Triage | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L1-Triage.md` |
| Cloud L2 Investigation | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L2-Investigation.md` |
| Cloud L3 Forensics | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-L3-Forensics.md` |
| Cloud AWS Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-AWS-Specific.md` |
| Cloud Azure Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Azure-Specific.md` |
| Cloud GCP Specific | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-GCP-Specific.md` |
| APT Campaign Playbooks | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md` |
| Network Intrusion Playbooks | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md` |
| MITRE ATT&CK Quick Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md` |
| TTP Intelligence Report | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md` |
| IoC Output Register | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 21-May-2026 | SOC Manager / Threat Detection Team / Incident Response Team | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**