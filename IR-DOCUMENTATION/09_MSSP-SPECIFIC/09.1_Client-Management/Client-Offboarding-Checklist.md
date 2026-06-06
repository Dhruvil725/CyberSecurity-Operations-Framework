# Client Offboarding Checklist (MSSP)

---

# 1. Document Control

| Field          | Value                                             |
| -------------- | ------------------------------------------------- |
| Document Name  | Checklist – Client Offboarding                    |
| Document ID    | MSSP-CM-003                                       |
| Version        | 1.0                                               |
| Effective Date | 30-May-2026                                       |
| Owner          | MSSP Service Delivery Manager (SDM) / SOC Manager |
| Approved By    | CISO                                              |
| Classification | Confidential – Client Restricted                  |
| Review Cycle   | Annually                                          |

---

# 2. Purpose

This document provides the standardized **Client Offboarding Checklist** used by the MSSP to ensure structured, complete, and contractually compliant disengagement from client engagements.

A formal client offboarding process is critical because:

- improper offboarding creates data leakage risk, legal exposure, and regulatory non-compliance
- client data must be securely returned, transferred, or destroyed per contract and law
- NIST CSF Identify (ID.GV, ID.SC) functions require structured supply chain offboarding
- ISO 27001 Annex A.5.10 (Acceptable use), A.5.11 (Return of assets), A.5.34 (Privacy and PII) apply
- RBI Cyber Security Framework and outsourcing guidelines mandate structured exit
- DPDP Act and other privacy laws require data deletion upon engagement termination
- contractual obligations (data return, evidence handover, knowledge transfer) must be fulfilled
- multi-tenant environments require strict de-provisioning to prevent residual access
- audit trail required for compliance and dispute resolution
- intellectual property (custom playbooks, detection rules) must be handled per contract
- residual access via tools, integrations, and credentials must be eliminated
- knowledge transfer enables client continuity post-disengagement
- forensic and evidence artifacts have legal retention requirements

This checklist ensures:

- consistent offboarding process across all client disengagements
- complete coverage of operational, technical, contractual, and legal handover
- defined ownership and timelines for each offboarding activity
- audit-ready evidence of complete and compliant offboarding
- structured handover to incoming MSSP or in-house SOC
- protection of client data and MSSP intellectual property
- closure of operational, financial, and contractual obligations
- linkage to data segregation, evidence handling, and retention policies

Reference alignment:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`

---

# 3. Scope

This checklist applies to:

| Offboarding Scenario      | Examples                                       |
| ------------------------- | ---------------------------------------------- |
| **Contract Expiry**       | End of contract term, non-renewal              |
| **Client Termination**    | Client terminates for cause/convenience        |
| **MSSP Termination**      | MSSP terminates engagement                     |
| **Service Tier Change**   | Significant reduction in services scope        |
| **Acquisition/Merger**    | Client acquired by entity using different MSSP |
| **MSSP Replacement**      | Client switches to another MSSP                |
| **In-Sourcing**           | Client moves SOC operations in-house           |
| **Partial Offboarding**   | Specific services discontinued                 |
| **Emergency Termination** | Termination due to dispute/breach              |

Out of scope:

- Routine service modifications within existing contract (covered by change management)
- Temporary service suspensions (covered separately)
- Internal MSSP service tier changes that don't affect client

---

# 4. Definitions

| Term                       | Definition                                                     |
| -------------------------- | -------------------------------------------------------------- |
| Offboarding                | Structured disengagement of MSSP from client environment       |
| Effective Termination Date | Contractual date on which services formally end                |
| Transition Period          | Time between termination notice and effective date             |
| Knowledge Transfer (KT)    | Structured handover of operational knowledge                   |
| Data Handover              | Return of client data to client or incoming MSSP               |
| Data Destruction           | Secure deletion of client data per retention policy            |
| Residual Data              | Data legally required to be retained post-offboarding          |
| De-Provisioning            | Removal of MSSP access from client environment                 |
| Exit Report                | Final report summarizing service delivery and offboarding      |
| Legal Hold                 | Retention requirement overriding standard destruction          |
| Tenant De-Activation       | Removal of client tenant from multi-tenant MSSP infrastructure |
| Successor                  | Incoming MSSP or in-house team taking over                     |

---

# 5. Roles and Responsibilities

| Role                             | Responsibilities                                               |
| -------------------------------- | -------------------------------------------------------------- |
| MSSP SDM                         | Primary owner of offboarding; coordinates all activities       |
| SOC Manager                      | Approves offboarding plan; validates technical de-provisioning |
| MSSP CISO                        | Approves data destruction; final sign-off                      |
| Legal Counsel                    | Reviews contractual obligations; advises on data handling      |
| Compliance Lead                  | Validates regulatory compliance of offboarding                 |
| MSSP Onboarding/Offboarding Lead | Executes operational offboarding tasks                         |
| Detection Engineer               | De-provisions client-specific detection rules                  |
| Threat Intel Analyst             | Archives client-specific TI artifacts                          |
| L1/L2/L3 Analysts                | Complete pending tickets; participate in KT                    |
| Documentation Custodian          | Archives client documentation per retention                    |
| IT/Infra Team                    | De-provisions infrastructure access                            |
| Finance                          | Final billing reconciliation                                   |
| Client Primary Contact           | Validates handover; receives data; confirms completion         |
| Client Successor (if applicable) | Receives KT and operational handover                           |

---

# 6. Offboarding Principles (Mandatory)

| Principle                 | Requirement                                            |
| ------------------------- | ------------------------------------------------------ |
| Contract-driven           | All actions per contractual obligations                |
| Compliance-driven         | Per regulatory requirements (RBI, DPDP, ISO, etc.)     |
| Confidentiality preserved | Client data protected throughout process               |
| Documented                | All actions logged with evidence                       |
| Time-bound                | Per contractual timelines                              |
| Verified                  | Two-person verification for critical actions           |
| Tenant-scoped             | Strict separation maintained until tenant decommission |
| Auditable                 | Complete audit trail maintained                        |
| Knowledge preserved       | KT enables client continuity                           |
| Disputes avoided          | Clear communication and acknowledgments                |

---

# 7. Offboarding Timeline (Standard)

> Timeline varies per contract; below is standard 90-day offboarding.

| Phase                           | Days         | Activities                                      |
| ------------------------------- | ------------ | ----------------------------------------------- |
| **Phase 1: Notification**       | T-90 to T-75 | Termination notice; offboarding plan            |
| **Phase 2: Planning**           | T-75 to T-60 | Detailed plan; KT plan; data handling decisions |
| **Phase 3: Knowledge Transfer** | T-60 to T-30 | Structured KT to client/successor               |
| **Phase 4: Service Wind-Down**  | T-30 to T-7  | Reduce service intensity; close pending items   |
| **Phase 5: Final Cutover**      | T-7 to T-0   | Final handover; service termination             |
| **Phase 6: Post-Termination**   | T+0 to T+30  | Data handover/destruction; final reports        |
| **Phase 7: Closure**            | T+30 to T+90 | Final reconciliation; archive; legal closeout   |

---

# 8. Offboarding Checklist (Copy/Paste)

## 8.1 Offboarding Initiation (Mandatory)

### 8.1.1 Notification

- [ ] Termination notice received/issued (party initiating: Client / MSSP / Mutual)
- [ ] Notice acknowledged in writing
- [ ] Effective termination date confirmed: `[YYYY-MM-DD]`
- [ ] Reason for termination documented: `[Expiry / Non-renewal / Termination for cause / etc.]`
- [ ] Termination notification logged in MSSP system
- [ ] CISO notified
- [ ] Legal counsel notified
- [ ] Compliance lead notified
- [ ] SDM appointed as Offboarding Lead

### 8.1.2 Offboarding Kickoff Meeting

- [ ] Offboarding kickoff meeting scheduled
- [ ] Attendees: Client primary contact + SDM + SOC Manager + Legal + Successor (if known)
- [ ] Termination scope confirmed (full / partial)
- [ ] Effective dates aligned
- [ ] High-level handover plan agreed
- [ ] Communication protocol agreed
- [ ] Single point of contact (SPOC) confirmed on both sides
- [ ] Kickoff meeting minutes documented and circulated

---

## 8.2 Contractual and Legal Review (Mandatory)

### 8.2.1 Contract Review

- [ ] Master Services Agreement (MSA) reviewed
- [ ] Statement of Work (SOW) reviewed
- [ ] Data Processing Agreement (DPA) reviewed
- [ ] Service Level Agreement (SLA) reviewed
- [ ] Non-Disclosure Agreement (NDA) post-termination obligations reviewed
- [ ] Exit clauses identified and documented
- [ ] Data return/destruction obligations identified
- [ ] Retention obligations identified (legal/regulatory)
- [ ] Penalty / liquidated damages considerations reviewed
- [ ] IP ownership clarified (custom playbooks, detection rules, reports)
- [ ] Survival clauses noted (confidentiality, indemnification, etc.)

### 8.2.2 Regulatory Compliance Review

- [ ] RBI outsourcing guidelines compliance verified (if BFSI client)
- [ ] DPDP Act / privacy law obligations identified
- [ ] Industry-specific requirements identified (PCI, HIPAA, etc.)
- [ ] Data residency requirements confirmed for destruction
- [ ] Regulatory notification requirements identified (if any)

### 8.2.3 Legal Approvals

- [ ] Legal counsel sign-off on offboarding plan
- [ ] Data handling approach approved by Legal
- [ ] Any legal holds identified and documented
- [ ] Any pending disputes flagged
- [ ] Indemnification considerations addressed

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

## 8.3 Offboarding Plan Document (Mandatory)

### 8.3.1 Plan Components

- [ ] Detailed offboarding plan document created
- [ ] Plan reviewed with client
- [ ] Plan approved by client (written acknowledgment)
- [ ] Plan approved by MSSP SOC Manager + CISO
- [ ] Plan includes:
  - [ ] Timeline and milestones
  - [ ] Roles and responsibilities (RACI)
  - [ ] Knowledge transfer plan
  - [ ] Data handling plan (return / destruction)
  - [ ] De-provisioning plan
  - [ ] Communication plan
  - [ ] Risk mitigation plan
  - [ ] Exit reporting plan
  - [ ] Final acceptance criteria

---

## 8.4 Service Continuity During Transition (Mandatory)

### 8.4.1 Service Levels Maintained

- [ ] SLAs maintained until effective termination date
- [ ] No degradation of service confirmed
- [ ] On-call coverage maintained
- [ ] Incident response capability maintained
- [ ] Reporting continued per contract
- [ ] Client informed of any planned scope changes

### 8.4.2 Open Incidents Management

- [ ] All open incidents inventoried
- [ ] Closure plan for each open incident
- [ ] Incidents that may not close before termination identified
- [ ] Handover plan for incidents transitioning to successor
- [ ] Documentation completed for all incidents

### 8.4.3 Pending Tickets and Requests

- [ ] All open tickets inventoried
- [ ] Closure plan agreed
- [ ] Tickets transitioning to successor identified
- [ ] Status reports provided to client

---

## 8.5 Knowledge Transfer (Mandatory)

### 8.5.1 KT Plan Development

- [ ] KT plan developed in consultation with client/successor
- [ ] KT timeline agreed
- [ ] KT formats agreed (workshops / documentation / shadow operations)
- [ ] KT recipients identified

### 8.5.2 KT Sessions

- [ ] **Session 1: Environment Overview**
  - [ ] Client environment walkthrough
  - [ ] Architecture review
  - [ ] Asset register handover
  - [ ] Date conducted: `___` | Attendees: `___`
- [ ] **Session 2: Operations Overview**
  - [ ] SOC operations walkthrough
  - [ ] Tool configurations explained
  - [ ] Log source map handover
  - [ ] Date conducted: `___` | Attendees: `___`
- [ ] **Session 3: Detection and Playbooks**
  - [ ] Custom detection rules walkthrough
  - [ ] Custom playbooks handover
  - [ ] Tuning history shared
  - [ ] Date conducted: `___` | Attendees: `___`
- [ ] **Session 4: Threat Intelligence**
  - [ ] Threat landscape briefing for client
  - [ ] Relevant actor profiles handover
  - [ ] Historical IoCs handover
  - [ ] Date conducted: `___` | Attendees: `___`
- [ ] **Session 5: Incident History**
  - [ ] Significant incidents walkthrough
  - [ ] Lessons learned summary
  - [ ] Outstanding improvement actions
  - [ ] Date conducted: `___` | Attendees: `___`
- [ ] **Session 6: Operational Procedures**
  - [ ] Escalation procedures
  - [ ] Reporting procedures
  - [ ] Routine operations
  - [ ] Date conducted: `___` | Attendees: `___`
- [ ] **Session 7: Q&A and Shadow Operations**
  - [ ] Successor shadow operations completed (if applicable)
  - [ ] Open questions addressed
  - [ ] Final clarifications
  - [ ] Date conducted: `___` | Attendees: `___`

### 8.5.3 KT Documentation Handover

- [ ] Client Environment Profile (sanitized of MSSP-internal content)
- [ ] Asset register
- [ ] Log source map
- [ ] Detection rule library (per IP ownership)
- [ ] Custom playbooks (per IP ownership)
- [ ] Tuning history and rationale
- [ ] Threat intelligence artifacts relevant to client
- [ ] Incident history reports
- [ ] Lessons learned register
- [ ] Improvement action tracker (outstanding items)
- [ ] Standard operating procedures
- [ ] Escalation matrices
- [ ] Contact directories (client-owned content)

### 8.5.4 KT Acknowledgment

- [ ] KT plan executed completely
- [ ] Client/successor acknowledgment of KT received in writing
- [ ] KT gaps documented (if any)
- [ ] Remediation of KT gaps agreed (if any)

---

## 8.6 Data Handling – Return, Transfer, Destruction (Mandatory)

### 8.6.1 Data Inventory

- [ ] Complete inventory of client data in MSSP possession
- [ ] Data categorized by:
  - [ ] Telemetry/log data
  - [ ] Incident artifacts and evidence
  - [ ] Forensic images
  - [ ] Reports
  - [ ] Configuration data
  - [ ] Threat intelligence artifacts
  - [ ] Email/communication records
  - [ ] Backup data
- [ ] Data storage locations identified
- [ ] Data classification confirmed
- [ ] Retention requirements per data type identified

### 8.6.2 Data Return / Transfer

- [ ] Client preference confirmed: Return / Transfer to successor / Destruction
- [ ] Transfer format agreed (raw / processed / standard format)
- [ ] Transfer mechanism agreed (secure portal / encrypted media / S3 / SFTP)
- [ ] Encryption keys exchanged (if applicable)
- [ ] Transfer chunks defined for large volumes
- [ ] Transfer schedule agreed
- [ ] Data transferred per agreed schedule
- [ ] Transfer completion confirmed by recipient
- [ ] Integrity validation (hashes) performed
- [ ] Transfer log maintained
- [ ] Transfer acknowledgment received in writing

### 8.6.3 Data Destruction

- [ ] Destruction scope confirmed (what to destroy after transfer)
- [ ] Destruction method per data type:
  - [ ] Cloud storage – cryptographic erasure / deletion + verification
  - [ ] On-prem storage – DoD-grade wipe / physical destruction
  - [ ] Backup media – per backup destruction SOP
  - [ ] Memory/RAM – power cycling + clearing
  - [ ] Printed materials – cross-cut shredding
- [ ] Destruction performed by authorized personnel
- [ ] Two-person verification for destruction
- [ ] Destruction certificate generated
- [ ] Certificate signed by:
  - [ ] Destruction operator
  - [ ] Verifier (witness)
  - [ ] CISO (final approval)
- [ ] Destruction certificate provided to client
- [ ] Destruction log maintained in audit records

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

### 8.6.4 Residual Data Handling

> Data legally/contractually required to be retained.

- [ ] Residual data inventory created
- [ ] Retention period per item documented
- [ ] Storage location and access controls confirmed
- [ ] Retention rationale documented (legal / regulatory / contractual)
- [ ] Client notified of residual retention
- [ ] Future destruction schedule established
- [ ] Access restricted to authorized personnel only

### 8.6.5 Evidence and CoC Records

- [ ] Evidence inventory specific to client
- [ ] Chain-of-Custody records reviewed
- [ ] Evidence relevant to ongoing legal/regulatory matters identified
- [ ] Evidence transfer plan to client (or successor) agreed
- [ ] Evidence retention/destruction per legal advice
- [ ] CoC handover documented

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`

---

## 8.7 De-Provisioning (Mandatory)

### 8.7.1 MSSP Access Removal from Client Environment

- [ ] All MSSP user accounts in client environment identified
- [ ] All MSSP service accounts in client environment identified
- [ ] All API keys/tokens issued to MSSP identified
- [ ] All VPN access for MSSP removed
- [ ] All cloud access (IAM roles, federation) removed
- [ ] All EDR/SIEM admin access removed
- [ ] All ticketing system access removed
- [ ] All documentation portal access removed
- [ ] Bastion/jumphost access removed
- [ ] Removal verified by client
- [ ] De-provisioning evidence provided to client

### 8.7.2 Client Access Removal from MSSP Environment

- [ ] All client user accounts in MSSP portal identified
- [ ] Client portal access disabled
- [ ] Client SIEM dashboard access removed (if applicable)
- [ ] Client TI feed access removed
- [ ] Client API access removed
- [ ] Client SSO federation removed
- [ ] Client access removal verified

### 8.7.3 Integration Decommissioning

- [ ] All MSSP-client integrations inventoried:
  - [ ] Log forwarders / syslog
  - [ ] EDR cloud-to-cloud
  - [ ] SIEM-to-SIEM
  - [ ] API integrations
  - [ ] SOAR/ticketing integrations
  - [ ] Threat intel feed integrations
  - [ ] Email forwarding rules
- [ ] Decommissioning schedule agreed
- [ ] Integrations stopped per schedule
- [ ] Confirmation of decommissioning
- [ ] No residual data flow verified

### 8.7.4 Network Connectivity Termination

- [ ] Site-to-site VPN tunnels identified
- [ ] Dedicated circuits identified (if any)
- [ ] Termination schedule agreed
- [ ] Connectivity terminated per schedule
- [ ] Firewall rules removed (both sides)
- [ ] Network configuration documented for record

### 8.7.5 Credential Rotation (Client Side)

- [ ] All credentials shared with MSSP rotated by client:
  - [ ] Administrative passwords
  - [ ] Service account passwords
  - [ ] API keys
  - [ ] Shared secrets
  - [ ] Certificates
- [ ] Rotation completion confirmed
- [ ] PAM records updated

---

## 8.8 Tool and License Disposition (Mandatory)

### 8.8.1 MSSP-Owned Tools

- [ ] Tools deployed in client environment by MSSP identified
- [ ] Removal/transfer decision agreed:
  - [ ] Remove from client environment
  - [ ] Transfer ownership (if contractually allowed)
  - [ ] Retain for ongoing service (partial offboarding)
- [ ] Tools removed/transferred per plan
- [ ] License terminations confirmed with vendors

### 8.8.2 Client-Owned Tools (MSSP-Managed)

- [ ] Tools identified
- [ ] Management responsibility transitioned to client/successor
- [ ] Configuration handover completed
- [ ] License records handover completed

### 8.8.3 Shared/Hybrid Licensing

- [ ] Shared licensing arrangements reviewed
- [ ] Disposition agreed
- [ ] Vendors notified
- [ ] Contracts updated

---

## 8.9 Multi-Tenant De-Provisioning (Mandatory)

### 8.9.1 SIEM Tenant De-Activation

- [ ] Client tenant identified in SIEM
- [ ] Data export per retention plan
- [ ] Tenant indexes/data deletion scheduled
- [ ] Tenant configuration archived
- [ ] Tenant deactivated post-retention period
- [ ] Two-person verification of deactivation

### 8.9.2 SOAR / Ticketing De-Activation

- [ ] Client workspace identified in SOAR/ticketing
- [ ] Open tickets closed/transferred
- [ ] Workflow rules disabled
- [ ] Client workspace archived
- [ ] Workspace deletion scheduled per retention

### 8.9.3 TI Platform De-Activation

- [ ] Client-specific TI artifacts identified
- [ ] Client feed access removed
- [ ] Client-specific IoCs archived
- [ ] Client tenant deactivated

### 8.9.4 Other Multi-Tenant Tools

- [ ] All other multi-tenant platforms (EDR, NDR, etc.) reviewed
- [ ] Client tenant de-provisioning per tool
- [ ] Verification documented

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

## 8.10 Reporting and Documentation (Mandatory)

### 8.10.1 Final Service Reports

- [ ] Final monthly report provided
- [ ] Final SLA compliance report provided
- [ ] Final incident summary report provided
- [ ] Final threat intel summary provided
- [ ] All pending reports completed and delivered

### 8.10.2 Exit Report

- [ ] Exit Report drafted including:
  - [ ] Service summary over engagement period
  - [ ] Incidents handled (high-level statistics)
  - [ ] SLA performance summary
  - [ ] Improvements delivered
  - [ ] Outstanding items
  - [ ] Knowledge transfer summary
  - [ ] Data handover/destruction summary
  - [ ] De-provisioning confirmation
  - [ ] Recommendations to client
- [ ] Exit Report reviewed by SOC Manager
- [ ] Exit Report approved by CISO
- [ ] Exit Report delivered to client
- [ ] Client acknowledgment received

### 8.10.3 Documentation Archival

- [ ] Client documentation inventoried
- [ ] Retention requirements per document confirmed
- [ ] Documents archived per retention
- [ ] Documents destruction scheduled per retention
- [ ] Archive index maintained

---

## 8.11 Financial Closure (Mandatory)

### 8.11.1 Final Billing

- [ ] All services through termination date invoiced
- [ ] Pro-rata calculations (if applicable) confirmed
- [ ] Any pending credits applied
- [ ] Final invoice sent to client
- [ ] Payment terms confirmed
- [ ] Disputes (if any) resolved

### 8.11.2 Refunds and Adjustments

- [ ] Pre-paid services refunds calculated (if applicable)
- [ ] Refunds processed
- [ ] SLA credits applied
- [ ] Reconciliation complete

### 8.11.3 Final Settlement

- [ ] Final payment received from client (or refund issued)
- [ ] Books closed for engagement
- [ ] Finance system updated

---

## 8.12 Communication and Stakeholder Management (Mandatory)

### 8.12.1 Internal MSSP Communications

- [ ] SOC team notified of offboarding
- [ ] Detection engineering notified
- [ ] Threat intel team notified
- [ ] Finance team notified
- [ ] Legal team notified
- [ ] Sales/Account team notified
- [ ] Client removal from internal portals/lists

### 8.12.2 Client Communications

- [ ] Periodic offboarding status updates to client
- [ ] Communication of any blockers or delays
- [ ] Final completion notification
- [ ] Post-offboarding contact for queries provided

### 8.12.3 Successor MSSP Communications (if applicable)

- [ ] Initial introduction by client
- [ ] Joint planning meetings as needed
- [ ] Technical handover sessions
- [ ] Q&A support during transition
- [ ] Final closure with successor

---

## 8.13 Personnel and Resource Reassignment (Mandatory)

- [ ] Assigned SOC personnel reassigned
- [ ] SDM transitioned
- [ ] Knowledge captured in MSSP knowledge base for future reference
- [ ] Lessons learned from engagement captured
- [ ] Resource capacity updated in MSSP planning

---

## 8.14 Final Acceptance and Sign-Off (Mandatory)

### 8.14.1 Pre-Closure Checklist

- [ ] All offboarding plan items completed
- [ ] All data handled per plan (returned/destroyed)
- [ ] All de-provisioning completed
- [ ] All KT delivered
- [ ] Exit Report delivered
- [ ] Final billing reconciled
- [ ] All documentation archived

### 8.14.2 Client Acceptance

- [ ] Client final acceptance form sent
- [ ] Client confirmation received in writing
- [ ] Acceptance form includes:
  - [ ] Confirmation of data return/destruction
  - [ ] Confirmation of access removal
  - [ ] Confirmation of KT completion
  - [ ] Confirmation of Exit Report receipt
  - [ ] No outstanding issues statement
  - [ ] Signature of authorized client representative

### 8.14.3 MSSP Final Sign-Off

- [ ] SDM sign-off
- [ ] SOC Manager sign-off
- [ ] Compliance Lead sign-off
- [ ] Legal Counsel sign-off
- [ ] CISO final sign-off
- [ ] Offboarding closure logged

---

## 8.15 Post-Offboarding Activities (Mandatory)

### 8.15.1 Post-Termination Support (per Contract)

- [ ] Post-termination support obligations identified
- [ ] Support availability documented (typically 30-90 days)
- [ ] Limited query support provided as agreed
- [ ] Knowledge base availability confirmed

### 8.15.2 Lessons Learned (MSSP Internal)

- [ ] Offboarding lessons learned session conducted
- [ ] Improvement opportunities documented
- [ ] Process improvements implemented
- [ ] Documentation updated

### 8.15.3 Reference and Testimonial (if Applicable)

- [ ] Reference request to client (if amicable termination)
- [ ] Case study development (per client approval)
- [ ] Testimonial request (per client approval)

---

# 9. Special Scenarios

## 9.1 Emergency / For-Cause Termination

For termination due to disputes, breach, or emergency:

| Activity           | Modification                               |
| ------------------ | ------------------------------------------ |
| Timeline           | Accelerated (may be days vs months)        |
| Legal involvement  | Heightened; legal-led approach             |
| Documentation      | More rigorous; assume potential litigation |
| Data handling      | Conservative; legal hold likely            |
| Communications     | Through legal counsel                      |
| Knowledge transfer | May be limited                             |
| Final acceptance   | May be contested                           |

Additional steps:

- [ ] Legal hold immediately implemented
- [ ] All communications via legal channels
- [ ] Evidence preservation prioritized
- [ ] Documentation of disputed items
- [ ] Escalation to executive leadership

## 9.2 Partial Offboarding

For scope reduction (not full termination):

- [ ] Scope changes precisely documented
- [ ] Updated SOW signed
- [ ] Only impacted services offboarded
- [ ] Continuing services unaffected
- [ ] Updated SLAs for continuing services
- [ ] Updated billing reflects scope reduction

## 9.3 Acquisition/Merger Scenarios

When client is acquired by entity using different MSSP:

- [ ] Acquiring entity's MSSP relationship considered
- [ ] Joint planning with both MSSPs (if needed)
- [ ] Smooth transition prioritized
- [ ] Confidentiality preserved
- [ ] Data handling per acquiring entity's policies

---

# 10. Data Retention Schedule (Reference)

> Per MSSP retention policy; client contract may override.

| Data Type            | Standard Retention Post-Offboarding       | Notes                       |
| -------------------- | ----------------------------------------- | --------------------------- |
| Telemetry/logs       | Per client decision (typically destroyed) |                             |
| Incident records     | 7 years (regulatory typical)              | Per RBI/sector requirements |
| Evidence (CoC)       | Per legal advice; minimum 3 years         |                             |
| Forensic images      | Per legal advice                          |                             |
| Reports              | 7 years                                   |                             |
| Contracts/SOWs       | 7 years post-termination                  |                             |
| Financial records    | Per applicable tax/finance law            |                             |
| Email/communications | 3 years (typical)                         |                             |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`

---

# 11. Risks and Mitigations (Standard)

| Risk                                   | Mitigation                                    |
| -------------------------------------- | --------------------------------------------- |
| Data leakage during handover           | Encrypted transfer; integrity verification    |
| Incomplete de-provisioning             | Comprehensive checklist; verification         |
| Service degradation pre-termination    | SLA monitoring; dedicated SDM focus           |
| Knowledge loss                         | Structured KT program; documentation handover |
| Dispute over scope/billing             | Clear contract review; documented agreements  |
| Residual access via integrations       | Comprehensive integration inventory           |
| Regulatory non-compliance              | Compliance review; legal sign-off             |
| Reputation damage                      | Professional handover; reference quality      |
| Successor MSSP issues                  | Joint planning; clear handover artifacts      |
| Personnel attrition during offboarding | Resource planning; key person continuity      |

---

# 12. Quality Checklist (Per Offboarding)

Before declaring offboarding complete:

- [ ] All items in Section 8 completed and checked
- [ ] All sign-offs obtained (client + MSSP)
- [ ] Data handling (return/destruction) verified
- [ ] All access removed (both directions)
- [ ] All integrations decommissioned
- [ ] All credentials rotated (by client)
- [ ] Multi-tenant resources de-provisioned
- [ ] Exit Report delivered and acknowledged
- [ ] Final billing reconciled
- [ ] Documentation archived per retention
- [ ] Lessons learned captured
- [ ] Offboarding closure documented

---

# 13. Offboarding Closure Document (Mandatory)

| Field                          | Value                                    |
| ------------------------------ | ---------------------------------------- |
| Offboarding ID                 | `OFF-CL-####`                            |
| Client Name                    |                                          |
| Client ID                      |                                          |
| Contract Start Date            |                                          |
| Contract End Date              |                                          |
| Termination Reason             |                                          |
| Offboarding Start Date         |                                          |
| Offboarding End Date           |                                          |
| Total Engagement Duration      |                                          |
| SDM (Offboarding)              |                                          |
| Data Disposition Summary       | Returned / Destroyed / Both / Retained   |
| Successor MSSP (if applicable) |                                          |
| Outstanding Items (if any)     |                                          |
| Final Status                   | Closed Successfully / Closed with Issues |

**Sign-Off:**

| Role                   | Name | Signature | Date |
| ---------------------- | ---- | --------- | ---- |
| MSSP SDM               |      |           |      |
| MSSP SOC Manager       |      |           |      |
| MSSP CISO              |      |           |      |
| MSSP Legal Counsel     |      |           |      |
| Client Primary Contact |      |           |      |
| Client CISO/Authorized |      |           |      |

---

# 14. MSSP Considerations (Mandatory)

Per MSSP multi-tenant operations:

- Strict tenant segregation maintained until full de-provisioning
- No information about offboarded client to be shared with other clients
- Knowledge gained may inform generic improvements but never client-specific cross-pollination
- Internal lessons learned must sanitize client identifiers
- Reference/case study only with explicit client written consent
- Continuing obligations (NDA, confidentiality) survive termination indefinitely

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 15. Integration with Other Processes

| Process                    | Integration Point                                    |
| -------------------------- | ---------------------------------------------------- |
| Client Onboarding          | Mirror process; lessons feed onboarding improvements |
| Client Environment Profile | Profile archived at offboarding                      |
| Client IR Contacts         | Contacts archived; access removed                    |
| Asset Register             | Handover and de-provisioning                         |
| Custom Playbooks           | Handover per IP ownership                            |
| Detection Rules            | Handover per IP ownership                            |
| Evidence Management        | Per legal/retention requirements                     |
| Data Segregation           | Strict until full de-provisioning                    |
| Audit Records              | Offboarding included in audit evidence               |
| Vendor Management          | Tool licensing disposition                           |

---

# 16. Related Documents

| Document                            | Path                                                                                            |
| ----------------------------------- | ----------------------------------------------------------------------------------------------- |
| Client Onboarding Checklist         | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`                        |
| Client Environment Profile Template | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`                |
| Client IR Contacts                  | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                                 |
| Client Asset Register Template      | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Asset-Register-Template.xlsx`                   |
| Client Data Segregation Policy      | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| Client-Specific Playbook Guide      | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`         |
| MSSP Client Evidence Handling       | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md`       |
| Evidence Destruction SOP            | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Destruction-SOP.md`            |
| Evidence Retention Schedule         | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md`         |
| Legal Counsel Engagement SOP        | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| MSSP-Client SLA Template            | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                                    |
| MSSP-Client Responsibility Matrix   | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`            |
| MSSP Monthly Client Report          | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Monthly-Client-Report.md`                           |
| MSSP SLA Compliance Report          | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md`                           |
| MSSP ISO27001 Controls              | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-ISO27001-Controls.md`                               |
| Audit Evidence Package              | `07_REPORTING/07.4_Regulatory-Reports/Audit-Evidence-Package.md`                                |

---

# 17. Revision History

| Version | Date        | Author                 | Changes         |
| ------- | ----------- | ---------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SDM / SOC Manager | Initial version |

---

# 18. Approval

Approved by (MSSP):

Name: ____________________
Title: ____________________
Date: ____________________

Acknowledged by (Client):

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
