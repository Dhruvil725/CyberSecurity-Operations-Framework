# Playbook: Ransomware – L1 Triage

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Ransomware (L1 Triage) |
| Document ID | IR-PB-RAN-002 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Lead / SOC Manager |
| Approved By | IR Team Lead / CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 ransomware incident |

---

## 2. Purpose

This document defines the L1 SOC Analyst procedure for triaging suspected ransomware activity. It provides:

- qualification steps (alert to incident)
- immediate validation checks
- required documentation and evidence capture
- severity recommendation rules (P1/P2/P3/P4)
- escalation requirements and timelines
- immediate containment requests (not execution unless pre-approved)

L1’s goal is to quickly answer:
- Is this real ransomware activity?
- Is encryption active?
- What is the minimum scope right now?
- Who must be engaged immediately?

---

## 3. Scope

Applies to ransomware alerts/events from:
- EDR (mass file modification/encryption)
- SIEM correlation rules
- file server monitoring (mass rename, high-entropy writes)
- backup platform alerts (backup deletion/tampering)
- user reports (files inaccessible, ransom note)
- network monitoring (lateral movement, C2 indicators)

This L1 playbook applies for:
- enterprise environments
- MSSP client environments (with client-specific SLAs and approval rules)

---

## 4. Preconditions and Safety Rules

1. Do not run remediation tools or delete artifacts.
2. Do not reboot affected systems unless instructed by IR Team/L3.
3. Do not access backups from potentially compromised hosts.
4. Do not communicate externally or to clients directly unless authorized by SOC Lead/SDM.
5. Preserve evidence first; take containment action only if pre-approved or directed.

Reference:
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`
- `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 5. Inputs (What L1 Must Collect)

Before making decisions, L1 must capture:

### 5.1 Alert Metadata (Mandatory)
- alert name and source (EDR/SIEM/file server)
- detection timestamp (UTC) and time observed
- affected hostnames and IP addresses
- affected user(s) (if applicable)
- rule ID / detection ID (if available)
- evidence snippet (log excerpt, EDR event summary)

### 5.2 Asset Context (Mandatory)
- asset type: endpoint / server / file share / domain controller / backup server
- business criticality: critical / high / standard (if known)
- environment: production / non-production
- owner/team: IT ops / application owner (if known)

### 5.3 High-Risk Indicators (As Applicable)
- ransom note filename(s)
- encrypted extension(s)
- shadow copy deletion indicators
- backup deletion indicators
- privilege account involvement indicators

---

## 6. L1 Triage SLA Targets (Ransomware)

| Severity | L1 Triage Target | Escalation Target |
|----------|------------------|-------------------|
| P1 | 5 minutes | SOC Lead immediately; L2 within 10 minutes |
| P2 | 10 minutes | SOC Lead immediately; L2 within 15 minutes |
| P3 | 15 minutes | L2 within 30 minutes if required |
| P4 | 30 minutes | close or batch as per SOP |

Reference:
- `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 7. Step-by-Step Triage Procedure (L1)

### Step 1: Confirm the Alert is Ransomware-Relevant (60–120 seconds)

Identify which signal triggered:

| Signal Type | Examples |
|------------|----------|
| EDR Behavioral | mass file rename/write, high-entropy file writes, suspicious process pattern |
| SIEM Rule | known ransomware process + suspicious command line behavior |
| File Server | rapid file renames, high volume writes, extension changes |
| Backup Platform | backup deletion, repository access anomalies |
| User Report | files inaccessible, ransom note found |

If the alert is not ransomware-relevant, reclassify under correct category.

---

### Step 2: Validate if Encryption is Active or Completed

Determine status using available telemetry:

- Are file extensions changing rapidly?
- Are large numbers of files modified in a short time window?
- Is EDR reporting ongoing encryption behavior now?
- Is a ransom note being written repeatedly?

Record one of the following states in the ticket:
- Active encryption in progress
- Encryption completed (host appears impacted but no longer changing)
- Precursor stage suspected (no encryption yet; ransomware tools/behavior present)
- Unknown (insufficient data; escalate to L2)

---

### Step 3: Identify Minimum Scope (Fast Scoping)

L1 must identify:
- patient zero candidate (first host where activity detected)
- number of affected hosts known at triage time
- whether a file server or shared storage is impacted

Minimum scoping checks:
- search SIEM for same alert type across last 60 minutes
- check EDR console for other hosts with same detection
- identify whether the same user is associated across affected hosts

Output required in ticket:
- impacted host list (even if partial)
- suspected time window start/end

---

### Step 4: Check for Immediate P1 Triggers (Stop-and-Escalate)

If any are true, recommend P1 and notify SOC Lead immediately:

- ransom note found on a server or shared file storage
- active encryption on a server, file server, domain controller, or backup server
- shadow copies or backups deletion indicators
- multiple hosts impacted rapidly (spread)
- privileged account involvement suspected
- security tooling tampering suspected (EDR disabled, logs cleared)
- business-critical service disruption reported

Reference:
- `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md`
- `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Escalation-Criteria.md`

---

### Step 5: Assign Category and Severity Recommendation

- Category: CAT-01 Ransomware
- Severity recommendation based on evidence:

| Condition | Recommendation |
|----------|----------------|
| encryption active on any system | P1 |
| ransom note present | P1 |
| file share/server impacted | P1 |
| precursor activity only (no encryption) but high confidence | P2 |
| single endpoint suspicious but not confirmed | P3 |
| blocked/prevented; no execution | P4 |

L1 must explicitly state: "Recommended severity: P# due to: [reasons]".

---

### Step 6: Create / Update Ticket (Required Format)

L1 must create or update the ticket with:

- severity recommendation and justification
- affected assets list
- active encryption status (yes/no/unknown)
- evidence attachments
- actions taken (only triage actions at L1)
- escalation performed (who/when)

Use the ticket template in Section 10.

---

### Step 7: Escalate Correctly (Mandatory)

Escalation rules:
- Any P1/P2 ransomware suspicion: escalate to SOC Lead immediately and assign to L2
- If file server/DC/backup server is involved: escalate to IR Team through SOC Lead
- If MSSP client: notify SDM/SOC Lead to initiate client notification per SLA

Reference:
- `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`
- `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

## 8. L1 Allowed Actions (Without Additional Approval)

L1 may perform:
- ticket creation, enrichment, correlation checks
- initial IOC extraction (hashes/domains/IPs/file paths)
- evidence export/screenshot collection from tools
- request containment actions via SOC Lead

L1 must not perform (unless pre-approved by authority matrix):
- isolate production servers directly
- disable privileged accounts directly
- make firewall rule changes
- contact clients directly (MSSP) without SOC Lead/SDM process
- reimage or delete files

Reference:
- `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 9. Evidence to Capture at L1 (Minimum Set)

Attach to ticket (as applicable):

### 9.1 Endpoint Evidence (EDR)
- detection summary (name, time, confidence)
- process tree screenshot/export
- file activity summary (mass rename/write indicator)
- network connection summary (external IPs/domains)
- user context (logged-in user, parent process)

### 9.2 SIEM Evidence
- raw log excerpts supporting ransomware indicator
- correlation rule results
- query used (copy/paste into ticket)

### 9.3 File Server / Share Evidence (if applicable)
- sample of affected file paths
- extension changes observed
- first observed ransom note location and name

### 9.4 Ransom Note / Extension Evidence
- ransom note filename(s)
- sample of encrypted file extension(s)
- do not open ransom note on infected host; copy safely via approved method

### 9.5 Backup Evidence (if applicable)
- backup job anomalies
- repository access alerts
- deletion/tampering alerts

Reference:
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/`

---

## 10. Ticket Notes Template (Copy-Paste Standard)

Title:
- Ransomware suspected – [Host/Service] – [Client/Org] – [P# recommended]

Required fields:
- Alert Source:
- Alert Name / ID:
- Time Detected (UTC):
- Affected Host(s):
- Affected User(s):
- Asset Criticality:
- Environment (Prod/Non-Prod):
- Ransom Note Observed (Yes/No/Unknown):
- Encryption Activity (Active/Completed/Unknown):
- File Extension Observed:
- Evidence Captured (EDR/SIEM/Logs):
- Initial Scope (known hosts count):
- Recommended Severity:
- Recommended Category: CAT-01 Ransomware
- Escalations Made:
  - SOC Lead notified (time/method):
  - L2 assigned (time):
  - IR Team engaged (if applicable):
- Immediate Risks Identified:
- Actions Taken (L1):
- Actions Requested (Containment requests):

---

## 11. Escalation Message Template (Internal)

Use concise internal message to SOC Lead:

Subject:
- Ransomware suspected – [Host] – [P# recommended]

Body:
- Detection source and time:
- Host(s)/user(s):
- Encryption status (active/completed/unknown):
- Ransom note present (yes/no/unknown):
- Scope known so far:
- Recommended severity and why:
- Ticket link:

---

## 12. Common L1 Misclassifications to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| treating precursor tools as low severity | delayed response | classify as P2 and escalate |
| assuming blocked alert means no incident | missed infection | confirm no execution and no follow-on activity |
| not checking for share/server impact | delayed P1 | always verify if file shares affected |
| not capturing evidence before containment requests | weak investigation | attach minimum evidence set |
| delaying SOC Lead notification while gathering too much detail | SLA breach | escalate early; L2 can deepen scope |

---

## 13. MSSP Notes (Client Context)

For MSSP operations, L1 must:
- ensure correct client attribution and tenant ID
- avoid cross-client data exposure in screenshots/logs
- follow client SLA for notification initiation (via SOC Lead/SDM)
- document any client constraints (no isolation during business hours, etc.)

Reference:
- `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Multi-Client-Triage-MSSP.md`

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Ransomware Master Playbook | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md` |
| L2 Investigation | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L2-Investigation.md` |
| Containment | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md` |
| P1 Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md` |
| Severity Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Escalation Paths | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Lead / SOC Manager | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document