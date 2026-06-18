<div align="center">

# 🔐 OWASP ZAP – Web Application Security Assessment: DAST, Vulnerability Scanning & Exploitation Lab

![Domain](https://img.shields.io/badge/Security-Web%20Application%20Penetration%20Testing-red?style=for-the-badge)
![Tool](https://img.shields.io/badge/Tool-OWASP%20ZAP%202.17.0-blue?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-purple?style=for-the-badge)

<img src="https://img.shields.io/badge/OWASP%20ZAP-DAST-blue?style=flat-square" />
<img src="https://img.shields.io/badge/Target-testasp.vulnweb.com-red?style=flat-square" />
<img src="https://img.shields.io/badge/Findings-21%20Alerts-orange?style=flat-square" />
<img src="https://img.shields.io/badge/High%20Severity-6-critical?style=flat-square" />
<img src="https://img.shields.io/badge/Framework-OWASP%20Top%2010-green?style=flat-square" />
<img src="https://img.shields.io/badge/OS-Kali%20Linux-blueviolet?style=flat-square" />

---

**Prepared by:** Bikash Raya  
**Project Type:** Web Application Security Assessment – DAST Lab

</div>

---

## 📁 Repository Structure
 
| File | Description |
| --- | --- |
| [Web-App-Security-Assessment-OWASP-Lab.pdf](./Web-App-Security-Assessment-OWASP-Lab.pdf) | Complete lab report with screenshots and detailed findings |
| [Webtest-ZAP-Report-.html](./Webtest-ZAP-Report-.html) | Raw ZAP-generated scan report (all 21 alerts) |
| [Webtest-ZAP-Report.pdf](./Webtest-ZAP-Report.pdf) | PDF version of the ZAP-generated scan report |
| README.md | Project overview |

---

## 📋 Overview

This repository documents a hands-on **Dynamic Application Security Testing (DAST)** lab conducted against **testasp.vulnweb.com** — an intentionally vulnerable ASP.NET web application maintained by Acunetix for security training purposes.

The assessment was performed using **OWASP ZAP 2.17.0** on **Kali Linux**, following a structured penetration testing methodology that covered:

* 🔍 Web application reconnaissance and attack surface mapping
* 🕷️ Automated spidering to discover 19 unique endpoints
* ⚡ Active vulnerability scanning across all discovered resources
* 💉 Confirmed SQL Injection (including time-based blind injection)
* 🔥 Cross-Site Scripting — DOM-based and Reflected
* 📂 Path Traversal exposing Windows system files
* 🔗 Open Redirect exploitable for phishing
* 🛡️ Missing security headers and cookie misconfigurations
* 📝 Professional risk-based reporting with remediation guidance

---

## 🛠️ Technologies Used

* OWASP ZAP 2.17.0 (Zed Attack Proxy by Checkmarx)
* Kali Linux
* Firefox Browser
* curl / nslookup (Connectivity Validation)
* ASP.NET Target Application (testasp.vulnweb.com)
* Microsoft IIS 8.5
* HTTP / HTTPS Protocol Analysis
* OWASP Top 10 (2021) Framework
* CWE (Common Weakness Enumeration)

---

## 🧪 Lab Environment

| Component | Details | Role |
| --- | --- | --- |
| Attacker Machine | Kali Linux | Testing Platform |
| Security Tool | OWASP ZAP 2.17.0 | DAST Scanner |
| Target Application | testasp.vulnweb.com | Intentionally Vulnerable ASP.NET App |
| Web Server | Microsoft-IIS/8.5 | Target Infrastructure |
| Assessment Type | Dynamic Application Security Testing (DAST) | Methodology |

---

## 🌐 Assessment Architecture

```
[Kali Linux – Attacker Machine]
          ↓
[OWASP ZAP 2.17.0]
          ↓
[Traditional Spider → Site Discovery (19 Endpoints)]
          ↓
[Active Scanner → Vulnerability Testing]
          ↓
[Target: testasp.vulnweb.com (ASP.NET / IIS 8.5)]
          ↓
[ZAP Alerts Panel → 21 Findings]
          ↓
[Risk Analysis → Professional Report]
```

---

## 🔬 Assessment Phases

### Phase 1 — Environment Preparation

* Installed OWASP ZAP on Kali Linux via apt:

```bash
sudo apt install zaproxy -y
```

* Verified installation and launched ZAP GUI

### Phase 2 — Connectivity Verification

* DNS resolution confirmed:

```bash
nslookup testasp.vulnweb.com
```

* HTTP connectivity validated — server returned `HTTP/1.1 200 OK`:

```bash
curl -I http://testasp.vulnweb.com
```

* Response headers revealed technology stack (noted as information disclosure finding):
  * `Server: Microsoft-IIS/8.5`
  * `X-Powered-By: ASP.NET`

### Phase 3 — ZAP Configuration

* Configured target URL in ZAP Automated Scan
* Enabled Traditional Spider; disabled Ajax Spider
* Default scan policy applied (all vulnerability categories)

### Phase 4 — Site Discovery

ZAP Traditional Spider mapped **19 unique endpoints** including:

| Endpoint | Significance |
| --- | --- |
| `Login.asp` | Authentication endpoint — primary attack vector |
| `Search.asp` | Search functionality — SQLi & XSS vector |
| `showthread.asp` | Thread view — Reflected XSS injection point |
| `Templatize.asp` | Template loader — Path Traversal target |
| `Register.asp` | User registration — input validation target |
| `robots.txt / sitemap.xml` | Application structure disclosure |

### Phase 5 — Active Scanning

ZAP launched an active scan across all discovered resources, testing for:
* SQL Injection (error-based and time-based blind)
* Cross-Site Scripting (Reflected, DOM-based)
* Path Traversal / Local File Inclusion
* External / Open Redirect
* Security Header Misconfigurations
* Cookie Security Weaknesses
* Information Disclosure via HTTP Headers

### Phase 6 — Analysis & Reporting

* Reviewed all 21 alerts in the ZAP Alerts panel
* Classified findings by severity and OWASP Top 10 category
* Generated ZAP HTML report
* Authored professional security assessment report with screenshots

---

## 🚨 Vulnerability Findings Summary

| # | Vulnerability | Severity | Count | CWE |
| --- | --- | --- | --- | --- |
| 1 | SQL Injection | 🔴 High | 4 | CWE-89 |
| 2 | SQL Injection – MsSQL Time-Based Blind | 🔴 High | 3 | CWE-89 |
| 3 | Cross-Site Scripting – DOM Based | 🔴 High | 2 | CWE-79 |
| 4 | Cross-Site Scripting – Reflected | 🔴 High | 1 | CWE-79 |
| 5 | External Redirect (Open Redirect) | 🔴 High | 2 | CWE-601 |
| 6 | Path Traversal | 🔴 High | 2 | CWE-22 |
| 7 | Absence of Anti-CSRF Tokens | 🟠 Medium | 3 | CWE-352 |
| 8 | Content Security Policy Header Not Set | 🟠 Medium | 5 | CWE-693 |
| 9 | Missing Anti-Clickjacking Header | 🟠 Medium | 5 | CWE-1021 |
| 10 | HTTP Only Site | 🟠 Medium | 1 | — |
| 11 | Application Error Disclosure | 🟡 Low | 3 | CWE-209 |
| 12 | Cookie No HttpOnly Flag | 🟡 Low | 1 | CWE-1004 |
| 13 | Cookie Without SameSite Attribute | 🟡 Low | 1 | CWE-1275 |
| 14 | Server Version Disclosure (Server Header) | 🟡 Low | 5 | CWE-200 |
| 15 | X-Powered-By Header Disclosure | 🟡 Low | 5 | CWE-200 |
| 16 | X-Content-Type-Options Header Missing | 🟡 Low | 5 | CWE-693 |
| 17 | Information Disclosure – Debug Error Messages | 🟡 Low | 3 | CWE-200 |
| 18 | GET for POST | ℹ️ Informational | 1 | — |
| 19 | Suspicious Comments in Source Code | ℹ️ Informational | 1 | CWE-200 |
| 20 | Session Management Response Identified | ℹ️ Informational | 1 | — |
| 21 | User Agent Fuzzer | ℹ️ Informational | 5 | — |

---

## 💉 Critical Findings – Proof of Concept

### SQL Injection – Time-Based Blind (CWE-89)

ZAP confirmed time-based blind SQL injection on `Login.asp`. The payload caused a **15,220ms response delay** (vs 0ms baseline), confirming Microsoft SQL Server as the backend and that query execution time is fully attacker-controllable.

```
Parameter: tfUName (POST)
Payload:   ZAP) ' WAITFOR DELAY '0:0:15' --
Result:    Response time: 0ms → 15,220ms ✅ Confirmed
```

### Path Traversal (CWE-22)

ZAP confirmed the server returned actual contents of `Windows/system.ini` when a traversal sequence was supplied to `Templatize.asp`.

```
URL:      /Templatize.asp?item=../../../../../../../../Windows/system.ini
Response: [drivers]  wave=mmdrv.dll  timer=timer.drv  ✅ File contents returned
```

### Cross-Site Scripting – DOM Based (CWE-79)

Payload executed via URL fragment, bypassing all server-side input filters entirely.

```
URL:     /Search.asp?name=abc#<img src="x" onerror=alert(5397)>
Result:  JavaScript executed client-side ✅ Confirmed
```

### Cross-Site Scripting – Reflected (CWE-79)

```
Endpoint:  showthread.asp
Parameter: tfText (POST)
Payload:   </div><scrIpt>alert(1);</scRipt><div>
Result:    Script reflected verbatim in HTTP response ✅ Confirmed
```

### Open Redirect (CWE-601)

```
Request:  POST /Login.asp?RetURL=https://attacker.example.com
Response: HTTP/1.1 302 Object Moved → Location: https://attacker.example.com ✅ Confirmed
```

---

## 🛡️ Remediation Strategy

### Priority 1 — Critical (Immediate)

* **SQL Injection:** Replace all dynamic SQL with parameterized queries / prepared statements
* **XSS:** Implement server-side output encoding and a Content Security Policy header
* **Path Traversal:** Restrict `Templatize.asp` to an allow-listed set of templates; canonicalize all file paths
* **Open Redirect:** Validate `RetURL` against an internal URL allow-list only

### Priority 2 — High (Within 30 Days)

* Add CSRF tokens to all state-changing forms; set `SameSite=Strict` on session cookies
* Configure IIS to serve `Content-Security-Policy`, `X-Frame-Options`, `X-Content-Type-Options` headers globally
* Enable `HttpOnly` and `Secure` flags on all session cookies

### Priority 3 — Hardening (Ongoing)

* Suppress `Server` and `X-Powered-By` response headers
* Implement custom error pages; disable verbose debug errors in production
* Remove all developer comments from client-facing HTML and JavaScript

---

## 🎯 Skills Demonstrated

* Web Application Penetration Testing (DAST)
* OWASP ZAP Configuration & Active Scanning
* OWASP Top 10 (2021) Vulnerability Identification
* SQL Injection Detection & Analysis (Error-Based & Time-Based Blind)
* Cross-Site Scripting (DOM-Based & Reflected) Analysis
* Path Traversal & File Disclosure Exploitation
* Open Redirect Identification
* HTTP Protocol & Request/Response Analysis
* Attack Surface Mapping & Reconnaissance
* Risk Assessment & Severity Prioritisation
* Vulnerability Remediation Planning
* Kali Linux Security Tooling
* Professional Penetration Test Report Writing

---

## 🎯 Key Takeaway

> This project demonstrates practical, hands-on experience in web application security testing using OWASP ZAP — covering the full DAST lifecycle from environment setup and target reconnaissance through to active exploitation, evidence collection, risk-based analysis, and professional reporting. Critical OWASP Top 10 vulnerabilities including SQL Injection, XSS, Path Traversal, and Open Redirect were all confirmed with working proof-of-concept payloads against an intentionally vulnerable ASP.NET application.

---

## 🔗 Connect With Me

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/bikash-raya/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=for-the-badge&logo=github)](https://github.com/Bikash-Raya)

</div>

---

<div align="center">

⭐ If you find this project useful, feel free to star the repository ⭐

</div>
