# Client Onboarding Checklist (MSSP)

---

# 1. Document Control

| Field          | Value                                             |
| -------------- | ------------------------------------------------- |
| Document Name  | Checklist – Client Onboarding                     |
| Document ID    | MSSP-CM-004                                       |
| Version        | 1.0                                               |
| Effective Date | 30-May-2026                                       |
| Owner          | MSSP Service Delivery Manager (SDM) / SOC Manager |
| Approved By    | CISO                                              |
| Classification | Confidential – Client Restricted                  |
| Review Cycle   | Annually                                          |

---

# 2. Purpose

This document provides the standardized **Client Onboarding Checklist** used by the MSSP to ensure structured, complete, and contractually compliant initiation of new client engagements.

A formal client onboarding process is critical because:

- a structured onboarding establishes the foundation for service delivery quality
- incomplete onboarding leads to detection gaps, SLA breaches, and client dissatisfaction
- NIST CSF Identify (ID.AM, ID.GV, ID.SC) functions require comprehensive asset and governance understanding
- ISO 27001 Annex A.5.19–A.5.22 require supplier relationship and onboarding controls
- RBI Cyber Security Framework and outsourcing guidelines mandate structured engagement
- DPDP Act and other privacy laws require defined data processing arrangements
- contractual obligations (asset inventory, SLA baselining, scope definition) must be established
- multi-tenant environments require strict tenant provisioning to prevent contamination
- audit trail required for compliance and engagement validation
- regulatory requirements (RBI 2-6 hour reporting, CERT-In 6 hour) require pre-established processes
- service quality depends on accurate baseline environment knowledge
- staff orientation enables effective alert triage and response
- defined escalation paths must be operational from Day 1
- detection tuning requires environment baseline understanding

This checklist ensures:

- consistent onboarding process across all new client engagements
- complete coverage of contractual, technical, operational, and compliance aspects
- defined ownership and timelines for each onboarding activity
- audit-ready evidence of complete and compliant onboarding
- service-ready state at go-live with full operational capability
- foundation for client-specific playbook customization
- defined exit criteria for onboarding phase
- baseline for service measurement and improvement

Reference alignment:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`
`00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

# 3. Scope

This checklist applies to:

| Onboarding Scenario             | Examples                                          |
| ------------------------------- | ------------------------------------------------- |
| **New Client Acquisition**      | Net-new MSSP engagement                           |
| **Service Tier Expansion**      | Existing client adding new services               |
| **Geographic Expansion**        | Client adding new locations/regions               |
| **Subsidiary Addition**         | Adding subsidiaries to existing parent engagement |
| **Re-Engagement**               | Returning client (previously offboarded)          |
| **Acquisition Onboarding**      | Client acquired by entity using MSSP              |
| **Migration from Another MSSP** | Client switching to MSSP                          |
| **Partial Onboarding**          | Specific services initially                       |

Out of scope:

- Routine service modifications within existing scope (covered by change management)
- Internal MSSP service tier changes
- Sales/business development activities (covered by Sales/Account team)

---

# 4. Definitions

| Term                                  | Definition                                                           |
| ------------------------------------- | -------------------------------------------------------------------- |
| Onboarding                            | Structured initiation of MSSP engagement with new client             |
| Go-Live Date                          | Date on which MSSP services formally commence                        |
| Onboarding Period                     | Time between contract signing and go-live                            |
| Service Readiness                     | State at which MSSP can deliver contracted services                  |
| Baseline Period                       | Initial period for environment understanding (typically 30 days)     |
| Tenant Provisioning                   | Creation of client-specific resources in multi-tenant infrastructure |
| Discovery | Information gathering about client environment                       |
| Hyper-Care                            | Post-go-live intensive support period                                |
| Onboarding Acceptance                 | Formal client acknowledgment of onboarding completion                |
| Steady-State                          | Normal operations post-onboarding                                    |
| Quick Win                             | Early demonstrable value to client                                   |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                      |
| ------------------------ | ----------------------------------------------------- |
| MSSP SDM                 | Primary owner; coordinates all onboarding activities  |
| MSSP Onboarding Lead     | Executes operational onboarding tasks                 |
| SOC Manager              | Approves onboarding plan; validates service readiness |
| MSSP CISO                | Approves contract; final sign-off                     |
| Sales/Account Lead       | Hands over from contract to onboarding                |
| Legal Counsel            | Reviews contracts; advises on data handling           |
| Compliance Lead          | Validates regulatory compliance setup                 |
| Detection Engineer       | Configures client-specific detection rules            |
| Threat Intel Analyst     | Sets up client-relevant threat intel                  |
| L1/L2/L3 Analysts        | Receive client orientation; ready for operations      |
| Documentation Custodian  | Creates client documentation structure                |
| IT/Infra Team            | Provisions infrastructure access and integrations     |
| Finance                  | Sets up billing and contract terms                    |
| Client Primary Contact   | Provides environment access; validates setup          |
| Client Executive Sponsor | Provides strategic direction; approves milestones     |

---

# 6. Onboarding Principles (Mandatory)

| Principle         | Requirement                                         |
| ----------------- | --------------------------------------------------- |
| Contract-driven   | All activities per signed contract                  |
| Compliance-first  | Compliance requirements met before go-live          |
| Risk-based        | Critical assets prioritized for early coverage      |
| Phased            | Structured phases with exit criteria                |
| Documented        | All activities and decisions logged                 |
| Time-bound        | Per agreed onboarding timeline                      |
| Tenant-segregated | Strict tenant separation from Day 1                 |
| Verified          | Service readiness validated before go-live          |
| Quality-gated     | No phase progression without prior phase completion |
| Client-aligned    | Continuous client engagement and validation         |

---

# 7. Onboarding Timeline (Standard)

> Timeline varies per client complexity; below is standard 60-90 day onboarding.

| Phase                                   | Days          | Activities                                     |
| --------------------------------------- | ------------- | ---------------------------------------------- |
| **Phase 0: Pre-Onboarding**             | T-30 to T-0   | Contract finalization; sales handover          |
| **Phase 1: Kickoff & Planning**         | T+0 to T+7    | Kickoff meeting; detailed onboarding plan      |
| **Phase 2: Discovery**                  | T+7 to T+21   | Environment discovery; documentation           |
| **Phase 3: Provisioning & Integration** | T+21 to T+45  | Tenant setup; tool integration; log onboarding |
| **Phase 4: Configuration & Tuning**     | T+45 to T+60  | Detection tuning; playbook customization       |
| **Phase 5: Validation & Testing**       | T+60 to T+75  | End-to-end testing; tabletop validation        |
| **Phase 6: Go-Live**                    | T+75          | Formal service commencement                    |
| **Phase 7: Hyper-Care**                 | T+75 to T+105 | Intensive post-go-live support                 |
| **Phase 8: Transition to Steady-State** | T+105         | Onboarding closure; steady-state operations    |

---

# 8. Onboarding Checklist (Copy/Paste)

## 8.1 Phase 0: Pre-Onboarding (Mandatory)

### 8.1.1 Contract Finalization

- [ ] Master Services Agreement (MSA) signed
- [ ] Statement of Work (SOW) signed
- [ ] Service Level Agreement (SLA) finalized and signed
- [ ] Data Processing Agreement (DPA) signed
- [ ] Non-Disclosure Agreement (NDA) executed
- [ ] Service tier and scope clearly defined
- [ ] Contract effective date confirmed: `[YYYY-MM-DD]`
- [ ] Go-live target date confirmed: `[YYYY-MM-DD]`
- [ ] Contract stored in MSSP contract repository
- [ ] Contract reviewed by Legal Counsel

### 8.1.2 Sales-to-Delivery Handover

- [ ] Sales handover meeting conducted
- [ ] Sales handover document received covering:
  - [ ] Client background and context
  - [ ] Commercial terms summary
  - [ ] Service scope summary
  - [ ] Key client stakeholders identified
  - [ ] Sales commitments (verbal or in proposal)
  - [ ] Known constraints or special requirements
  - [ ] Pre-sales technical assessments
- [ ] SDM appointed as Onboarding Lead
- [ ] Onboarding kickoff scheduled

### 8.1.3 Internal Resource Allocation

- [ ] Client ID assigned in MSSP systems: `CL-####`
- [ ] SOC team assignment (L1/L2/L3 pool)
- [ ] SDM (Primary and Backup) assigned
- [ ] Detection Engineer assigned
- [ ] Threat Intel Analyst assigned (for relevant industries)
- [ ] Compliance Lead assigned (for regulated clients)
- [ ] Internal kickoff meeting scheduled

---

## 8.2 Phase 1: Kickoff & Planning (Mandatory)

### 8.2.1 Onboarding Kickoff Meeting

- [ ] Kickoff meeting scheduled within 7 days of contract signing
- [ ] Attendees: Client primary contact + executive sponsor + SDM + SOC Manager
- [ ] Kickoff agenda covers:
  - [ ] Engagement overview
  - [ ] Onboarding timeline
  - [ ] Roles and responsibilities (RACI)
  - [ ] Communication protocols
  - [ ] Success criteria
  - [ ] Risks and mitigations
- [ ] Single Point of Contact (SPOC) confirmed on both sides
- [ ] Kickoff meeting minutes documented and circulated
- [ ] Client acknowledgment received

### 8.2.2 Onboarding Plan Development

- [ ] Detailed onboarding plan document created
- [ ] Plan includes:
  - [ ] Timeline with milestones
  - [ ] Roles and responsibilities
  - [ ] Discovery requirements
  - [ ] Integration requirements
  - [ ] Tuning approach
  - [ ] Validation approach
  - [ ] Go-live criteria
  - [ ] Hyper-care plan
  - [ ] Communication plan
  - [ ] Risk mitigation plan
- [ ] Plan reviewed with client
- [ ] Plan approved by client (written acknowledgment)
- [ ] Plan approved by MSSP SOC Manager + CISO

### 8.2.3 Governance and Cadence Setup

- [ ] Weekly status meetings scheduled (during onboarding)
- [ ] Steering committee identified
- [ ] Steering committee meetings scheduled (typically bi-weekly during onboarding)
- [ ] Escalation contacts confirmed both sides
- [ ] Issue tracking mechanism agreed
- [ ] Project management tool/portal set up (if applicable)

---

## 8.3 Phase 2: Discovery (Mandatory)

### 8.3.1 Business Context Discovery

- [ ] Client business overview documented
- [ ] Industry and sub-industry classified
- [ ] Geographic operations mapped
- [ ] Critical business processes identified
- [ ] Peak business periods documented
- [ ] Crown jewels identified by client
- [ ] Business impact tiers established
- [ ] Customer-facing services identified

### 8.3.2 Regulatory and Compliance Discovery

- [ ] All applicable regulations identified:
  - [ ] RBI Cyber Security Framework
  - [ ] CERT-In Directions (2022)
  - [ ] ISO/IEC 27001
  - [ ] PCI-DSS
  - [ ] SEBI Cybersecurity Framework
  - [ ] IRDAI Information & Cyber Security
  - [ ] DPDP Act
  - [ ] GDPR / HIPAA (if applicable)
  - [ ] NCIIPC (if CII)
  - [ ] Other industry/geographic regulations
- [ ] Mandatory reporting obligations documented
- [ ] Compliance status (current state) documented
- [ ] Audit history reviewed
- [ ] Pending audit findings reviewed

References:
`07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

### 8.3.3 Technical Environment Discovery

- [ ] Environment type assessed (on-prem / cloud / hybrid / multi-cloud)
- [ ] Cloud platforms inventoried (AWS / Azure / GCP / OCI / etc.)
- [ ] SaaS platforms inventoried (M365 / Google Workspace / Salesforce / etc.)
- [ ] Asset categories quantified:
  - [ ] Servers (physical + virtual)
  - [ ] Endpoints
  - [ ] Mobile devices
  - [ ] Network devices
  - [ ] Cloud workloads
  - [ ] Applications
  - [ ] Databases
  - [ ] Identity stores
- [ ] Network topology documented
- [ ] Network diagrams obtained (from client)
- [ ] Critical applications inventoried
- [ ] Data sensitivity and classification documented

### 8.3.4 Security Tools Discovery

- [ ] Existing security tools inventoried:
  - [ ] SIEM
  - [ ] EDR / XDR
  - [ ] NDR / IDS / IPS
  - [ ] Firewall (perimeter and internal)
  - [ ] WAF
  - [ ] DDoS protection
  - [ ] Email security
  - [ ] Web proxy / SWG
  - [ ] CASB
  - [ ] DLP (endpoint and network)
  - [ ] IAM / SSO / PAM / MFA
  - [ ] Vulnerability management
  - [ ] Patch management
  - [ ] Threat intelligence platform
  - [ ] SOAR
  - [ ] CSPM / CNAPP
  - [ ] Container security
  - [ ] Backup / recovery
- [ ] Tool ownership documented (client / MSSP / shared)
- [ ] Tool access requirements for MSSP identified
- [ ] Tool integration feasibility assessed

### 8.3.5 Operational Context Discovery

- [ ] Maintenance windows documented
- [ ] Change management process understood
- [ ] Known false positive patterns documented
- [ ] Approved software/tools whitelisted
- [ ] Historical incident summary reviewed (if available)
- [ ] Previous MSSP transition information (if applicable)
- [ ] Operational pain points identified

### 8.3.6 Stakeholder Discovery

- [ ] All client stakeholders identified (per `Client-IR-Contacts.md`)
- [ ] Contact directory drafted
- [ ] Approval authorities documented
- [ ] Escalation paths confirmed
- [ ] 24x7 on-call coverage identified

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

### 8.3.7 Documentation Output

- [ ] Client Environment Profile draft completed
- [ ] Asset Register draft completed
- [ ] IR Contacts Directory draft completed
- [ ] Network/architecture diagrams obtained
- [ ] All discovery documentation reviewed with client

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Asset-Register-Template.xlsx`

---

## 8.4 Phase 3: Provisioning & Integration (Mandatory)

### 8.4.1 Multi-Tenant Provisioning

- [ ] Client tenant created in SIEM
- [ ] Client tenant created in SOAR/ticketing
- [ ] Client tenant created in TI platform
- [ ] Client tenant created in EDR (if applicable)
- [ ] Client tenant created in NDR (if applicable)
- [ ] Tenant naming standards followed
- [ ] Tenant access controls configured
- [ ] Tenant data segregation verified
- [ ] Two-person verification of tenant provisioning

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

### 8.4.2 Access Provisioning (MSSP to Client Environment)

- [ ] MSSP user accounts created in client environment (per access plan)
- [ ] MSSP service accounts created with least privilege
- [ ] API keys/tokens issued and securely stored
- [ ] VPN access configured
- [ ] Cloud access (IAM roles, federation) configured
- [ ] EDR/SIEM admin access configured
- [ ] Ticketing system access configured
- [ ] Documentation portal access configured
- [ ] Bastion/jumphost access configured (if applicable)
- [ ] Access tested and verified
- [ ] PAM records updated with credentials

### 8.4.3 Access Provisioning (Client to MSSP Environment)

- [ ] Client user accounts created in MSSP portal
- [ ] Client portal access configured
- [ ] Client SIEM dashboard access configured (per service tier)
- [ ] Client TI feed access configured
- [ ] Client API access configured (if applicable)
- [ ] Client SSO federation configured (if applicable)
- [ ] Access tested and verified

### 8.4.4 Log Source Onboarding

- [ ] Log source inventory prioritized (per criticality)
- [ ] Phase 1 log sources (critical) onboarded:
  - [ ] Windows Servers (DCs, critical servers)
  - [ ] Linux Servers (critical)
  - [ ] Endpoints (EDR)
  - [ ] Firewall (perimeter)
  - [ ] Active Directory / Entra ID
  - [ ] Critical applications
- [ ] Phase 2 log sources (high) onboarded:
  - [ ] Internal firewalls
  - [ ] WAF
  - [ ] Email security
  - [ ] Proxy / SWG
  - [ ] Cloud audit logs (CloudTrail / Activity Logs / Audit Logs)
  - [ ] VPN logs
- [ ] Phase 3 log sources (medium) onboarded:
  - [ ] DNS logs
  - [ ] DLP events
  - [ ] Database audit logs
  - [ ] Application logs
  - [ ] Container/Kubernetes
- [ ] Log parsing validated
- [ ] Log enrichment configured
- [ ] EPS (events per second) measured and within license
- [ ] Coverage gaps documented

References:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md`

### 8.4.5 EDR Deployment

- [ ] EDR deployment plan agreed
- [ ] EDR deployed to critical servers
- [ ] EDR deployed to standard servers
- [ ] EDR deployed to endpoints (phased rollout)
- [ ] EDR coverage measured (target: ≥95%)
- [ ] EDR exclusions configured (per client baseline)
- [ ] Containment authority configured (per matrix)
- [ ] Auto-response configured (if applicable)

References:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Deployment-Coverage-Check.md`

### 8.4.6 Integration Setup

- [ ] All MSSP-client integrations configured:
  - [ ] Log forwarders / syslog
  - [ ] EDR cloud-to-cloud
  - [ ] SIEM-to-SIEM (if applicable)
  - [ ] API integrations
  - [ ] SOAR/ticketing integrations
  - [ ] Threat intel feed integrations
  - [ ] Email forwarding rules (if applicable)
- [ ] Integration testing completed
- [ ] Integration monitoring configured
- [ ] Integration documentation completed

### 8.4.7 Network Connectivity

- [ ] Site-to-site VPN tunnels configured (if applicable)
- [ ] Dedicated circuits configured (if applicable)
- [ ] Firewall rules configured (both sides)
- [ ] Connectivity tested
- [ ] Redundancy configured (if applicable)

---

## 8.5 Phase 4: Configuration & Tuning (Mandatory)

### 8.5.1 Baseline Establishment

- [ ] 14-day baseline period initiated
- [ ] Normal traffic patterns documented
- [ ] Normal user behavior baselined
- [ ] Normal application behavior baselined
- [ ] Anomalies identified and validated with client
- [ ] False positive sources identified

### 8.5.2 Detection Rule Configuration

- [ ] Standard SIEM use cases enabled
- [ ] Client-specific detection rules developed (per environment)
- [ ] Industry-specific detection rules enabled (BFSI / Healthcare / etc.)
- [ ] Compliance-required detection rules enabled (RBI / PCI / etc.)
- [ ] Threat actor-specific rules enabled (per client relevance)
- [ ] MITRE ATT&CK coverage mapped and tracked

References:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

### 8.5.3 Alert Tuning

- [ ] Initial false positives identified
- [ ] Tuning iterations completed
- [ ] Alert thresholds adjusted
- [ ] Exclusions configured (with client approval)
- [ ] Alert priority calibrated to client environment
- [ ] False positive rate target met (<10% typical)

References:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`

### 8.5.4 Playbook Customization

- [ ] Standard playbooks reviewed for client applicability
- [ ] Client-specific playbook customizations identified
- [ ] Custom playbooks developed (per client requirements)
- [ ] Client-specific escalation paths embedded
- [ ] Client-specific containment authorities embedded
- [ ] Client-specific regulatory reporting integrated
- [ ] Custom playbooks reviewed with client
- [ ] Custom playbooks approved

References:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`

### 8.5.5 Threat Intelligence Configuration

- [ ] Client-relevant threat actors profiled
- [ ] Industry-specific threat intel feeds configured
- [ ] Geographic-specific threat intel configured
- [ ] Client-specific IoC feeds enabled
- [ ] TI integration with detection rules verified
- [ ] Threat landscape briefing prepared for client

References:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`
`08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`

### 8.5.6 SOAR Workflow Configuration

- [ ] Client-specific SOAR workflows configured
- [ ] Auto-enrichment workflows enabled
- [ ] Auto-response workflows configured (per authority matrix)
- [ ] Integration with client ticketing (if applicable)
- [ ] Workflow testing completed

### 8.5.7 Reporting Setup

- [ ] Daily report template customized
- [ ] Weekly report template customized
- [ ] Monthly report template customized
- [ ] SLA compliance report configured
- [ ] Executive briefing template customized
- [ ] Report distribution lists configured
- [ ] Report delivery method agreed (email / portal / both)
- [ ] Sample reports validated with client

References:
`07_REPORTING/07.3_MSSP-Client-Reports/`

---

## 8.6 Phase 5: Validation & Testing (Mandatory)

### 8.6.1 End-to-End Testing

- [ ] Log ingestion validated for all sources
- [ ] Detection rule firing validated (sample alerts)
- [ ] SOAR workflow execution validated
- [ ] Alert escalation tested
- [ ] Ticket creation tested
- [ ] Client notification tested (test alerts)
- [ ] Reporting delivery tested
- [ ] Portal access tested by client
- [ ] All integrations confirmed operational

### 8.6.2 Synthetic Attack Validation

- [ ] Atomic Red Team tests executed
- [ ] Detection coverage validated for key MITRE techniques
- [ ] Mean time to detect (MTTD) measured
- [ ] Detection gaps documented for post-go-live tuning

References:
`10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`

### 8.6.3 Tabletop Exercise

- [ ] Joint tabletop exercise scheduled
- [ ] Scenario aligned to client environment and likely threats
- [ ] Exercise conducted with client SOC team
- [ ] Decision points and authorities validated
- [ ] Escalation paths validated
- [ ] Communication protocols validated
- [ ] After-action report completed
- [ ] Findings incorporated into playbooks

References:
`10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`

### 8.6.4 Process Validation

- [ ] Incident response process tested end-to-end
- [ ] Regulatory reporting process tested (test submission preparation)
- [ ] Containment authority workflows validated
- [ ] Bridge call process tested
- [ ] Documentation generation validated

### 8.6.5 SLA Baselining

- [ ] Detection capability validated against SLA
- [ ] Response time capability validated
- [ ] Reporting timeliness validated
- [ ] Initial SLA baseline established

References:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

### 8.6.6 Service Readiness Review

- [ ] Service readiness checklist completed
- [ ] All critical onboarding items confirmed complete
- [ ] Open items risk-assessed
- [ ] Go-live recommendation prepared
- [ ] Service readiness review with SOC Manager + CISO
- [ ] Go-live approval obtained

---

## 8.7 Phase 6: Go-Live (Mandatory)

### 8.7.1 Go-Live Decision

- [ ] Go-live readiness confirmed
- [ ] Client confirmation obtained
- [ ] Go-live date confirmed
- [ ] Communication plan executed (internal + client)

### 8.7.2 Go-Live Activities

- [ ] Service formally commenced at agreed date/time
- [ ] 24x7 monitoring active
- [ ] All SOC tiers ready (L1/L2/L3 briefed)
- [ ] Go-live announcement sent (internal + client)
- [ ] Steering committee informed
- [ ] Status broadcasted to all stakeholders

### 8.7.3 Day-1 Validation

- [ ] First operational shift completed successfully
- [ ] All alerts triaged appropriately
- [ ] No service disruptions
- [ ] Client experience validated
- [ ] Day-1 issues logged and addressed

---

## 8.8 Phase 7: Hyper-Care (Mandatory)

> Intensive support typically for 30 days post-go-live.

### 8.8.1 Hyper-Care Setup

- [ ] Hyper-care period defined (typically 30 days)
- [ ] Dedicated SDM focus during hyper-care
- [ ] Daily client check-ins scheduled
- [ ] Issue tracking heightened
- [ ] Quick escalation paths active

### 8.8.2 Hyper-Care Activities

- [ ] Daily status calls with client
- [ ] Weekly executive updates
- [ ] Continuous tuning based on operational learnings
- [ ] False positive reduction actively pursued
- [ ] Detection gap analysis ongoing
- [ ] Process refinement based on operations

### 8.8.3 Hyper-Care Metrics

- [ ] Alert volume tracked
- [ ] False positive rate tracked
- [ ] Detection effectiveness tracked
- [ ] SLA performance tracked
- [ ] Client satisfaction tracked

### 8.8.4 Hyper-Care Exit

- [ ] Hyper-care exit criteria met
- [ ] Steady-state readiness confirmed
- [ ] Hyper-care closure meeting with client
- [ ] Transition to standard operations approved

---

## 8.9 Phase 8: Transition to Steady-State (Mandatory)

### 8.9.1 Operational Transition

- [ ] Standard meeting cadence established:
  - [ ] Daily operational sync (internal SOC)
  - [ ] Weekly status with client
  - [ ] Monthly business review
  - [ ] Quarterly executive briefing
  - [ ] Annual strategy session
- [ ] Standard reporting cadence active
- [ ] Standard escalation processes active
- [ ] Steady-state SLAs in effect

### 8.9.2 Improvement Roadmap

- [ ] Joint improvement roadmap developed
- [ ] Quick wins identified for first 90 days
- [ ] Medium-term improvements identified (3-6 months)
- [ ] Long-term improvements identified (6-12 months)
- [ ] Roadmap approved by client

### 8.9.3 Documentation Finalization

- [ ] Client Environment Profile finalized
- [ ] IR Contacts Directory finalized
- [ ] Asset Register finalized
- [ ] Custom playbooks documented and stored
- [ ] All detection rules documented
- [ ] All integrations documented
- [ ] All learnings captured

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

## 8.10 Final Acceptance and Sign-Off (Mandatory)

### 8.10.1 Pre-Closure Checklist

- [ ] All onboarding plan items completed
- [ ] Service operating per SLA
- [ ] Hyper-care successfully exited
- [ ] All documentation finalized
- [ ] All tuning iterations completed
- [ ] Improvement roadmap agreed

### 8.10.2 Client Acceptance

- [ ] Onboarding acceptance form sent to client
- [ ] Client confirmation received in writing
- [ ] Acceptance form includes:
  - [ ] Confirmation of service activation
  - [ ] Confirmation of access and integration
  - [ ] Confirmation of documentation handover
  - [ ] Confirmation of training/orientation completion
  - [ ] No outstanding critical issues statement
  - [ ] Signature of authorized client representative

### 8.10.3 MSSP Final Sign-Off

- [ ] SDM sign-off
- [ ] SOC Manager sign-off
- [ ] Compliance Lead sign-off
- [ ] CISO final sign-off
- [ ] Onboarding closure logged

---

# 9. Special Scenarios

## 9.1 Migration from Another MSSP

When client is switching from another MSSP:

| Additional Activity               | Notes                    |
| --------------------------------- | ------------------------ |
| Coordinate with outgoing MSSP     | If client requests       |
| Knowledge transfer from incumbent | Per client coordination  |
| Historical incident review        | From incumbent's reports |
| Existing playbook review          | If transferable          |
| Existing tuning history           | If accessible            |
| Parallel run period               | Recommended 7-14 days    |

Additional steps:

- [ ] Parallel monitoring period agreed
- [ ] Cutover plan documented
- [ ] Cutover communication plan
- [ ] Rollback plan defined

## 9.2 Acquisition Onboarding

When new client is acquired by entity using MSSP:

- [ ] Acquired entity's existing security state assessed
- [ ] Integration with parent MSSP scope planned
- [ ] Distinct compliance requirements addressed
- [ ] Brand/identity considerations handled
- [ ] Communication coordinated with parent

## 9.3 Rapid Onboarding (Emergency)

When onboarding is accelerated due to crisis:

- [ ] Risk-based prioritization
- [ ] Phase 1 (critical) log sources prioritized
- [ ] Critical detection rules first
- [ ] Tuning deferred to post-stabilization
- [ ] Heightened communication
- [ ] Executive sponsorship active

## 9.4 Co-Managed SOC Onboarding

When client retains SOC team:

- [ ] Shared responsibility model documented
- [ ] Joint workflows defined
- [ ] Joint tooling access configured
- [ ] Joint training conducted
- [ ] Joint escalation paths defined

---

# 10. Onboarding Success Criteria (Mandatory)

Onboarding is considered successful when:

| Criterion                           | Target                           |
| ----------------------------------- | -------------------------------- |
| All critical log sources onboarded  | ≥95% coverage                    |
| EDR deployment                      | ≥95% endpoint coverage           |
| SLA performance                     | Meeting all SLA targets          |
| False positive rate                 | <10% across alerts               |
| Client satisfaction                 | Positive (per client survey)     |
| Detection coverage                  | Aligned to MITRE ATT&CK priority |
| Documentation completeness          | 100% mandatory documents         |
| Tabletop exercise                   | Completed successfully           |
| First incident handled successfully | Per SLA                          |

---

# 11. Common Onboarding Risks and Mitigations (Standard)

| Risk                                  | Mitigation                                   |
| ------------------------------------- | -------------------------------------------- |
| Delayed log source onboarding         | Risk-based prioritization; phased approach   |
| High false positive rate at go-live   | Extended tuning period; baseline analysis    |
| Incomplete asset discovery            | Continuous discovery; client validation      |
| Stakeholder unavailability            | Multiple contacts; backup identification     |
| Integration challenges                | Pre-onboarding feasibility assessment        |
| Detection gap discovery               | Post-go-live tuning; improvement roadmap     |
| Cultural fit issues                   | Early engagement; communication protocols    |
| Scope creep                           | Strict change control; documented agreements |
| Tool licensing surprises              | Pre-onboarding validation                    |
| Compliance gap discovery              | Early compliance review                      |
| Client expectation mismatch           | Clear documentation; regular alignment       |
| Personnel attrition during onboarding | Resource backup planning                     |

---

# 12. Quality Checklist (Per Onboarding)

Before declaring onboarding complete:

- [ ] All items in Section 8 completed
- [ ] All sign-offs obtained (client + MSSP)
- [ ] All log sources onboarded per plan
- [ ] EDR deployment per target
- [ ] Detection rules configured and tuned
- [ ] Custom playbooks developed and approved
- [ ] Tabletop exercise completed
- [ ] Hyper-care successfully exited
- [ ] SLA baseline established
- [ ] All documentation finalized
- [ ] Multi-tenant provisioning verified
- [ ] Improvement roadmap agreed
- [ ] Client acceptance obtained
- [ ] Onboarding closure documented

---

# 13. Onboarding Closure Document (Mandatory)

| Field                            | Value                                        |
| -------------------------------- | -------------------------------------------- |
| Onboarding ID                    | `ONB-CL-####`                                |
| Client Name                      |                                              |
| Client ID                        |                                              |
| Contract Start Date              |                                              |
| Go-Live Date                     |                                              |
| Onboarding Duration (Days)       |                                              |
| Hyper-Care End Date              |                                              |
| Service Tier                     |                                              |
| SDM (Onboarding)                 |                                              |
| SDM (Steady-State)               |                                              |
| Critical Log Sources Onboarded   | Count / Target                               |
| EDR Coverage Achieved            | %                                            |
| Tabletop Conducted (Y/N)         |                                              |
| Open Items at Closure            | Count                                        |
| Improvement Roadmap Agreed (Y/N) |                                              |
| Final Status                     | Closed Successfully / Closed with Open Items |

**Sign-Off:**

| Role                   | Name | Signature | Date |
| ---------------------- | ---- | --------- | ---- |
| MSSP SDM               |      |           |      |
| MSSP SOC Manager       |      |           |      |
| MSSP Compliance Lead   |      |           |      |
| MSSP CISO              |      |           |      |
| Client Primary Contact |      |           |      |
| Client CISO/Authorized |      |           |      |

---

# 14. MSSP Considerations (Mandatory)

Per MSSP multi-tenant operations:

- Strict tenant segregation from Day 1 of provisioning
- Two-person verification of tenant provisioning
- No cross-client visibility for analysts (per scope)
- Client-specific access controls strictly enforced
- Client-confidential information isolated
- Generic learnings sanitized of client identifiers
- Sales handover information protected
- Pre-onboarding assessments treated as confidential

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`09_MSSP-SPECIFIC/09.4_MSSP-Compliance/`

---

# 15. Integration with Other Processes

| Process                    | Integration Point                   |
| -------------------------- | ----------------------------------- |
| Sales/Account Management   | Handover from sales                 |
| Contract Management        | Contract finalization               |
| Client Offboarding         | Mirror process; learnings exchange  |
| Client Environment Profile | Profile created during onboarding   |
| Client IR Contacts         | Directory created during onboarding |
| Custom Playbooks           | Developed during onboarding         |
| Detection Engineering      | Detection setup during onboarding   |
| Threat Intelligence        | Client-relevant TI setup            |
| Tabletop Exercises         | Conducted during onboarding         |
| SLA Management             | Baseline established                |
| Compliance                 | Regulatory setup                    |
| Finance                    | Billing setup                       |

---

# 16. Related Documents

| Document                            | Path                                                                                    |
| ----------------------------------- | --------------------------------------------------------------------------------------- |
| Client Offboarding Checklist        | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`               |
| Client Environment Profile Template | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`        |
| Client IR Contacts                  | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                         |
| Client Asset Register Template      | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Asset-Register-Template.xlsx`           |
| Client Data Segregation Policy      | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`       |
| Client-Specific Playbook Guide      | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md` |
| Multi-Client Alert Handling         | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`          |
| MSSP-Client SLA Template            | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                            |
| MSSP-Client Responsibility Matrix   | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`    |
| SIEM Integration Map                | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md`                             |
| EDR Deployment Coverage Check       | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Deployment-Coverage-Check.md`                     |
| SIEM Use Cases Master               | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`                            |
| SIEM Alert Tuning Guide             | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`                          |
| TI Feed Management                  | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`                |
| Tabletop Exercise Guide             | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`          |
| Internal-to-MSSP Escalation         | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  |
| MSSP Monthly Client Report          | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Monthly-Client-Report.md`                   |
| MSSP ISO27001 Controls              | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-ISO27001-Controls.md`                       |
| MSSP Audit Readiness Checklist      | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`               |

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


