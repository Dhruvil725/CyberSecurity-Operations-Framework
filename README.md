# CyberSecurity-Operations-Framework

> **Enterprise-Grade Incident Response Documentation Framework**  
> Built for SOC Analysts · MSSP Operations · Cybersecurity Teams  
> Aligned with ISO 27001 | NIST CSF | RBI Cyber Security Framework | CERT-In

---

## What Is This?

This repository is a **complete, production-ready Incident Response (IR) documentation system** built from the ground up for real SOC and MSSP operations. It covers everything from governance and policy down to analyst-level SOPs, playbooks, forensic procedures, regulatory reporting, and post-incident improvement  393 files across 12 modules.

**This is not a template collection. This is an operational IR framework.**

Whether you're a solo SOC analyst building your first formal IR process, an MSSP onboarding a new client, or a security manager preparing for an ISO 27001 audit  this repository gives you the full structure, ready to adapt and deploy.

---

## Who This Is For

| Role | How You Use This |
|------|-----------------|
| **SOC Analyst (L1/L2/L3)** | Daily alert handling, shift checklists, escalation criteria, triage decision trees, SIEM/EDR investigation SOPs |
| **IR Team Member** | Playbooks per incident type, containment procedures, evidence chain-of-custody, onsite/remote response SOPs |
| **SOC Lead / IR Manager** | Escalation management, bridge call SOPs, client communication, KPI tracking, shift management |
| **MSSP / Managed Security Provider** | Multi-tenant procedures, client onboarding/offboarding, SLA templates, client playbook customization, multi-client alert handling |
| **Security Manager / CISO** | Governance policies, framework mappings, compliance readiness, regulatory reporting (RBI, CERT-In, ISO 27001) |
| **Compliance / Audit Team** | ISO 27001 Annex A mapping, NIST CSF controls, RBI CSF alignment, audit evidence packages |
| **Threat Intelligence Analyst** | IoC registers, TTP intelligence reports, threat actor profiles, TI feed management |
| **Trainer / Educator** | Onboarding programs (L1/L2/L3/IRT), tabletop exercise scenarios (ransomware, APT, insider threat, data breach), drills |
| **Students / Learners** | Real-world IR documentation to study how professional SOC operations are structured |

---

## Repository Stats

| Metric | Count |
|--------|-------|
| Total Files | 393 |
| Incident Response Playbooks | 88 |
| Playbook Categories Covered | 13 |
| Framework Mappings Included | ISO 27001, NIST CSF, RBI CSF |
| SOC Tier Procedure Sets | 5 (L1 / L2 / L3 / SOC Lead / IRT) |
| Tabletop Exercise Scenarios | 4 (Ransomware, APT, Data Breach, Insider Threat) |
| Regulatory Reporting SOPs | CERT-In, RBI, ISO 27001 |

---

## Repository Structure

```
IR-DOCUMENTATION/
├── 00_GOVERNANCE/                     # Policies, framework mappings, roles, SLAs
│   ├── 00.1_Policies/
│   ├── 00.2_Frameworks-Mapping/
│   ├── 00.3_Roles-and-Responsibilities/
│   └── 00.4_SLA-and-SLO/
│
├── 01_INCIDENT-CLASSIFICATION/        # Severity matrix, 14 incident categories, triage trees
│   ├── 01.1_Severity-Matrix/
│   ├── 01.2_Incident-Categories/
│   └── 01.3_Triage-Decision-Trees/
│
├── 02_PLAYBOOKS/                      # Full playbooks for 13 attack categories
│   ├── 02.0_Playbook-Index.md
│   ├── 02.1_Ransomware/
│   ├── 02.2_Phishing-BEC/
│   ├── 02.3_Malware-Trojan/
│   ├── 02.4_DDoS/
│   ├── 02.5_Insider-Threat/
│   ├── 02.6_Data-Breach-Exfiltration/
│   ├── 02.7_Credential-Attack/
│   ├── 02.8_Web-Application-Attack/
│   ├── 02.9_Supply-Chain-Attack/
│   ├── 02.10_Cloud-Security-Incident/
│   ├── 02.11_Network-Intrusion/
│   ├── 02.12_Zero-Day-Exploit/
│   └── 02.13_APT-Campaign/
│
├── 03_SOC-TIER-PROCEDURES/            # Role-specific SOPs for every SOC tier
│   ├── 03.1_L1-Procedures/
│   ├── 03.2_L2-Procedures/
│   ├── 03.3_L3-Procedures/
│   ├── 03.4_SOC-Lead-Procedures/
│   └── 03.5_IR-Team-Procedures/
│
├── 04_TOOLS-AND-TECHNOLOGY/           # SIEM, EDR, ticketing, TI, firewall, forensics
│   ├── 04.1_SIEM/
│   ├── 04.2_EDR/
│   ├── 04.3_Ticketing/
│   ├── 04.4_Threat-Intelligence/
│   ├── 04.5_Firewall-Network/
│   └── 04.6_Forensics-Tools/
│
├── 05_ESCALATION-AND-COMMUNICATION/   # Escalation paths, comm templates, regulatory comms
│   ├── 05.1_Escalation-Paths/
│   ├── 05.2_Communication-Templates/
│   ├── 05.3_Regulatory-Communication/
│   └── 05.4_Contact-Directory/
│
├── 06_EVIDENCE-AND-CHAIN-OF-CUSTODY/ # Evidence collection, CoC forms, storage policy
│   ├── 06.1_Evidence-Collection/
│   ├── 06.2_Chain-of-Custody/
│   └── 06.3_Evidence-Storage/
│
├── 07_REPORTING/                      # All IR report templates + regulatory reports
│   ├── 07.1_Incident-Reports/
│   ├── 07.2_Operational-Reports/
│   ├── 07.3_MSSP-Client-Reports/
│   └── 07.4_Regulatory-Reports/
│
├── 08_POST-INCIDENT/                  # PIR, RCA, improvement tracking, threat intel output
│   ├── 08.1_Lessons-Learned/
│   ├── 08.2_Root-Cause-Analysis/
│   ├── 08.3_Improvement-Tracking/
│   └── 08.4_Threat-Intel-Output/
│
├── 09_MSSP-SPECIFIC/                  # MSSP operations, client management, multi-tenancy
│   ├── 09.1_Client-Management/
│   ├── 09.2_Client-Playbook-Customization/
│   ├── 09.3_Multi-Tenant-Procedures/
│   └── 09.4_MSSP-Compliance/
│
├── 10_TRAINING-AND-EXERCISES/         # Onboarding programs, TTX scenarios, drills, knowledge base
│   ├── 10.1_Onboarding/
│   ├── 10.2_Tabletop-Exercises/
│   ├── 10.3_Drills/
│   └── 10.4_Knowledge-Base/
│
└── 11_ARCHIVE/                        # Closed incidents, retired playbooks, audit records
    ├── 11.1_Closed-Incidents/
    ├── 11.2_Retired-Playbooks/
    └── 11.3_Audit-Records/
```

---

## Module Breakdown

### 00 · Governance

The policy and governance foundation. Covers the IR master policy, framework alignment documents, role definitions across L1–L3–SOC Lead–IRT, MSSP client responsibility matrix, and complete SLA/SLO definitions.

**Key files:**
- `IR-Policy-Master.md`  Master IR policy (doc ID: IR-POL-001)
- `IR-Policy-ISO27001-Alignment.md`, `IR-Policy-NIST-Alignment.md`, `IR-Policy-RBI-Alignment.md`
- `RACI-Matrix-IR.xlsx`  Full RACI across all IR roles
- `MSSP-Client-SLA-Template.md`  SLA definitions per client tier
- `SLA-Breach-Escalation-Procedure.md`  What happens when SLAs are breached

---

### 01 · Incident Classification

P1/P2/P3/P4 severity definitions, 14 named incident category profiles, and triage decision trees for alert-to-incident qualification.

**14 Incident Categories:**
`Ransomware` · `Phishing/BEC` · `Malware/Trojan` · `DDoS` · `Insider Threat` · `Data Breach/Exfiltration` · `Credential Attack` · `Web Application Attack` · `Supply Chain Attack` · `Cloud Security Incident` · `Network Intrusion` · `Zero-Day Exploit` · `APT Campaign` · `Physical Security Incident`

---

### 02 · Playbooks

The operational core. 88 playbook files covering 13 attack types. Every playbook category contains:

- **Master Playbook**  Full IR lifecycle for the incident type
- **L1 Triage**  What the first-responder analyst does
- **L2 Investigation**  Deep-dive analysis procedures
- **L3 Forensics**  Advanced forensic and malware analysis
- **Containment**  Immediate and strategic containment steps
- **MITRE ATT&CK Mapping**  Full TTP mapping for threat hunting support
- **Specialized documents**  Vendor coordination, cloud-provider-specific (AWS/Azure/GCP), eradication, recovery, legal notification, ISP coordination, and more

---

### 03 · SOC Tier Procedures

Day-to-day operating procedures for every tier.

| Tier | What's Covered |
|------|---------------|
| **L1** | Alert handling SOP, shift checklist, SIEM/EDR response, ticket creation, escalation criteria, false positive handling, shift handover |
| **L2** | Investigation SOP, log analysis, network forensics, EDR deep investigation, evidence handling, threat hunting, shift handover |
| **L3** | Advanced forensics, disk/memory forensics, malware analysis, root cause analysis, technical report writing, threat intel integration |
| **SOC Lead** | Escalation management, P1/P2 bridge call SOP, incident coordination, client communication (MSSP), KPI tracking, shift management |
| **IR Team** | Activation criteria, containment authority matrix, evidence chain of custody, forensic collection, onsite/remote response, closure criteria |

---

### 04 · Tools & Technology

Operational guides for the core SOC toolchain.

| Category | Documents |
|----------|-----------|
| **SIEM** | Use cases master, query library, alert tuning guide, integration map, troubleshooting SOP |
| **EDR** | Alert handling guide, containment commands, investigation queries, exclusion management, deployment coverage check |
| **Ticketing** | Lifecycle SOP, fields standards, priority matrix, escalation workflow, closure criteria |
| **Threat Intelligence** | Feed management, IoC handling, SIEM/EDR integration, platform usage guide, reporting template |
| **Firewall/Network** | Block request SOP, rule change process, IDS/IPS tuning, network capture, isolation procedure |
| **Forensics Tools** | Disk/memory acquisition SOPs, log collection, forensics toolkit reference, tool chain of custody |

---

### 05 · Escalation & Communication

Full escalation path matrix (L1→L2→L3→IRT→Management), communication templates for every IR milestone, regulatory communication procedures, and a complete contact directory.

**Communication Templates Included:**
P1 Initial Alert · P2 Initial Alert · 30-min Status Update · 1-hour Status Update · Management Notification · MSSP Client Notification · Bridge Call Agenda · Incident Closure Notification

**Regulatory SOPs:**
- `CERT-In-Reporting-SOP.md`  Indian CERT-In mandatory incident reporting
- `RBI-Incident-Reporting-SOP.md`  RBI cyber incident reporting (6-hour requirement)
- `RBI-Report-Template.md`  Ready-to-use RBI report format

---

### 06 · Evidence & Chain of Custody

Procedures for collecting, transferring, and retaining digital and physical evidence. Includes ready-to-use chain-of-custody forms.

---

### 07 · Reporting

Every report template you'll need:

- **Incident Reports:** Initial, Interim, Final, Executive Summary, Technical Deep Dive
- **Operational Reports:** Daily SOC Report, Weekly Incident Summary, Monthly Metrics, Quarterly Trend Analysis, Annual IR Review
- **MSSP Client Reports:** Monthly Client Report, SLA Compliance Report, Executive Briefing, MSSP Incident Report
- **Regulatory Reports:** ISO 27001 Incident Log, NIST Incident Report, RBI Mandatory Report, Audit Evidence Package

---

### 08 · Post-Incident

Post-Incident Review (PIR) meeting agenda, lessons learned template and register (`.xlsx`), 5-Why and full RCA templates, action item tracker, playbook update log, and control gap tracker.

---

### 09 · MSSP-Specific

Built specifically for Managed Security Service Providers running multi-client SOC operations.

| Sub-module | Contents |
|------------|----------|
| **Client Management** | Client Asset Register (`.xlsx`), Environment Profile Template, IR Contacts Directory, Onboarding Checklist, Offboarding Checklist |
| **Client Playbook Customization** | Template structure for building client-specific playbooks under `CLIENT-NAME/` |
| **Multi-Tenant Procedures** | Data segregation policy, cross-client incident procedure, multi-client alert handling |
| **MSSP Compliance** | Audit readiness checklist, ISO 27001 controls for MSSPs, NIST alignment |

---

### 10 · Training & Exercises

| Sub-module | Contents |
|------------|----------|
| **Onboarding Programs** | L1, L2, L3, and IR Team onboarding programs with learning paths and competency checklists |
| **Tabletop Exercises** | Ransomware TTX, APT TTX, Data Breach TTX, Insider Threat TTX, Evaluation Scorecard, Exercise Guide |
| **Drills** | Annual drill schedule, Purple Team exercise guide, Red Team IR integration SOP, After Action Report template |
| **Knowledge Base** | MITRE ATT&CK quick reference, Attack technique reference, Common IoC reference, Tool command reference |

---

### 11 · Archive

Structured archive for closed incidents (`YYYY/MM/INC-ID-TYPE-DATE/`), retired playbook versions, and historical audit records.

---

## Framework Alignment

| Framework | Coverage |
|-----------|----------|
| **ISO/IEC 27001:2022** | Annex A.5.9 (Asset Management), A.5.24–A.5.28 (Incident Management), A.8.15–A.8.16 (Logging & Monitoring) |
| **NIST Cybersecurity Framework** | ID.AM, PR.IP, DE.AE, DE.CM, RS.*, RC.* |
| **RBI Cyber Security Framework** | Incident reporting timelines, regulatory communication SOPs, report templates |
| **CERT-In** | Mandatory incident reporting SOP (IT Amendment Rules 2022) |
| **MITRE ATT&CK** | Full TTP mapping in every playbook category |

---

## How to Use This Repository

### For SOC Analysts
1. Your starting point is `03_SOC-TIER-PROCEDURES/` → navigate to your tier (L1/L2/L3)
2. When an incident fires, go to `02_PLAYBOOKS/` → find the relevant category → open the **Master Playbook** first, then your tier's triage/investigation file
3. Check `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/` when you're unsure how to classify an alert

### For IR Team Members
1. Activation criteria: `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`
2. Evidence collection: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`
3. Communication: `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

### For MSSPs
1. Onboard a new client: `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`
2. Fill the client asset register: `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Asset-Register-Template.xlsx`
3. Customize playbooks: `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/CLIENT-NAME/`
4. Run multi-client ops: `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

### For Managers / CISOs
1. Review the governance layer: `00_GOVERNANCE/`
2. Check framework alignment: `00_GOVERNANCE/00.2_Frameworks-Mapping/`
3. Use audit evidence: `07_REPORTING/07.4_Regulatory-Reports/Audit-Evidence-Package.md`

### For Trainers
1. Onboarding programs: `10_TRAINING-AND-EXERCISES/10.1_Onboarding/`
2. Run a tabletop: `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/`
3. Knowledge base for self-study: `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/`

---

## File Naming Conventions

| Prefix | Meaning |
|--------|---------|
| `PB-` | Playbook |
| `L1-`, `L2-`, `L3-` | SOC tier-specific document |
| `SOCLead-` | SOC Lead procedure |
| `IRT-` | IR Team procedure |
| `MSSP-` | MSSP-specific document |
| `TI-` | Threat Intelligence |
| `RCA-` | Root Cause Analysis |
| `TTX-` | Tabletop Exercise |
| `CoC-` | Chain of Custody |
| `SLA-` / `SLO-` | Service Level Agreement / Objective |
| `CAT-` | Incident Category profile |

---

## Document Standards

All documents in this repository follow:

- **Document Control Block**  Document ID, Version, Owner, Effective Date, Review Cycle, Classification
- **Classification Levels**  `Public` · `Internal` · `Confidential` · `Restricted`
- **Review Cycle**  Annual (policies), Quarterly (MSSP operations), After major incidents (playbooks)
- **Version Control**  All documents are versioned; major revisions tracked in the document header

---

## Contributing / Adapting

This framework is designed to be adapted to your organisation's environment. When you use it:

1. **Replace placeholder fields**  Look for `[CLIENT NAME]`, `[CL-####]`, `[REDACT]`, `[fill]`, and similar markers across all documents
2. **Update contact directories**  `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/`
3. **Customise SLAs**  `00_GOVERNANCE/00.4_SLA-and-SLO/` to match your client agreements
4. **Map to your toolchain**  Update SIEM, EDR, and ticketing references throughout `04_TOOLS-AND-TECHNOLOGY/`
5. **Add client folders**  Copy `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/CLIENT-NAME/` per client

---

## Author

**Dhruvil** | Cybersecurity Analyst |

- Focus: SOC Operations · Incident Response · MSSP · Threat Detection

---

## License

This documentation framework is shared for educational and professional reference purposes. All content is original. If you adapt it for organisational use, please maintain the document control standards included in each file.

---

*Built with discipline. Designed for operations. Ready for the real thing.*
