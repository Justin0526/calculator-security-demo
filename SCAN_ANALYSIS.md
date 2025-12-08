# Security Scan Analysis - [03/12/2025]

## DAST Results (ZAP Baseline)
- Total URLs scanned: 3
- PASS: 61 checks
- WARN-NEW: 9 warnings
- FAIL-NEW: 0 failures

### Warning Summary
#### Medium Severity
| Warning Name | ZAP Code | Instances | 
|--------------|----------|-----------|
| Content Security Policy (CSP) Header Not Set | 10038 | 5 |
| HTTP Only Site | 10106 | 1 |
| Missing Anti-clickjacking Header | 10020 | 2 |

#### Low Severity
| Warning Name | ZAP Code | Instances |
|--------------|----------|-----------|
| Insufficient Site Isolation Against Spectre Vulnerability | 90004 | 6 |
| Permissions Policy Header Not Set | 10063 | 5 |
| Server Leaks Version Information via "Server" HTTP Response Header Field | 10036 | 5 |
| Strict-Transport-Security Header Not Set | 10035 | 1 |
| Timestamp Disclosure - Unix | 10096 | 1 |
| X-Content-Type-Options Header Missing | 10021 | 3 |


## SCA Results (Dependency Check)
- Total dependencies scanned: 2
- Vulnerable dependencies: 0
- High severity: 0
- Medium severity: 0
- Low severity: 0

### Vulnerable Packages
No vulnerable packages were identified by OWASP Dependency-Check.  
Both scanned dependencies (`flask==2.0.1` and `werkzeug==2.0.1`) have **0 known CVEs** at the time of the scan.

## SAST Results (CodeQL)
- Total issues: py/flask-debug
- By type: 
    - High severity: 1
    - Medium severity: 0
    - Low severity: 0
### Detected Issues
| File    | Line | Rule ID         | Severity | Description |
|---------|------|------------------|----------|-------------|
| app.py  | 40   | py/flask-debug   | High     | Flask application is running with debug mode enabled, which may allow remote code execution through the Werkzeug debugger. |

## Recommendations
## Remediation Recommendations

### 1. Disable Flask Debug Mode
Ensure that Flask applications that are run in a production environment have debugging disabled.

---

### 2. Content-Security-Policy Header
Ensure that your web server, application server, load balancer, etc. is configured to set the Content-Security-Policy header.

---

### 3. HTTP Only Site
Configure your web or application server to use SSL (https).

---

### 4. Anti-clickjacking Header
Modern Web browsers support the Content-Security-Policy and X-Frame-Options HTTP headers. Ensure one of them is set on all web pages returned by your site/app.

If you expect the page to be framed only by pages on your server (e.g. it's part of a FRAMESET) then you'll want to use SAMEORIGIN, otherwise if you never expect the page to be framed, you should use DENY. Alternatively consider implementing Content Security Policy's "frame-ancestors" directive.

---

### 5. Insufficient Site Isolation Against Spectre Vulnerability
Ensure that the application/web server sets the Cross-Origin-Resource-Policy header appropriately, and that it sets the Cross-Origin-Resource-Policy header to 'same-origin' for all web pages. 'same-site' is considered as less secured and should be avoided.

If resources must be shared, set the header to 'cross-origin'.

If possible, ensure that the end user uses a standards-compliant and modern web browser that supports the Cross-Origin-Resource-Policy header (https://caniuse.com/mdn-http_headers_cross-origin-resource-policy).

---

### 6. Permissions-Policy Header Not Set
Ensure that your web server, application server, load balancer, etc. is configured to set the Permissions-Policy header.

---

### 7. Server Leaks Version Information
Ensure that your web server, application server, load balancer, etc. is configured to suppress the "Server" header or provide generic details.

---

### 8. Strict-Transport-Security Header Not Set
Ensure that your web server, application server, load balancer, etc. is configured to enforce Strict-Transport-Security.

---

### 9. Timestamp Disclosure - Unix
Manually confirm that the timestamp data is not sensitive, and that the data cannot be aggregated to disclose exploitable patterns.

---

### 10. X-Content-Type-Options Header Missing
Ensure that the application/web server sets the Content-Type header appropriately, and that it sets the X-Content-Type-Options header to 'nosniff' for all web pages.

If possible, ensure that the end user uses a standards-compliant and modern web browser that does not perform MIME-sniffing at all, or that can be directed by the web application/web server to not perform MIME-sniffing.


## Intepret ZAP Findings
### Content Security Policy (CSP) Header Not Set  
**Risk:** Medium  
**Code:** 10038  

| Affected URL | Method | Why It Matters |
|--------------|--------|----------------|
| http://localhost:5000 | GET | CSP helps prevent XSS, data injection, and unauthorized content loading. |
| http://localhost:5000/ | GET | CSP helps prevent XSS, data injection, and unauthorized content loading. |
| http://localhost:5000/favicon.ico | GET | CSP helps prevent XSS, data injection, and unauthorized content loading. |
| http://localhost:5000/robots.txt | GET | CSP helps prevent XSS, data injection, and unauthorized content loading. |
| http://localhost:5000/sitemap.xml | GET | CSP helps prevent XSS, data injection, and unauthorized content loading. |

### HTTP Only Site  
**Risk:** Medium  
**Code:** 10106  

| Affected URL | Method | Other Info | Why It Matters |
|--------------|--------|------------|----------------|
| http://localhost:5000 | GET | Failed to connect. ZAP attempted to connect via: https://localhost:5000 | The site is only served under HTTP and not HTTPS. |

### Missing Anti-clickjacking Header  
**Risk:** Medium  
**Code:** 10020  

| Affected URL | Method | Parameter | Why It Matters |
|--------------|--------|-----------|----------------|
| http://localhost:5000 | GET | x-frame-options | The response does not protect against 'ClickJacking' attacks. |
| http://localhost:5000/ | GET | x-frame-options | The response does not protect against 'ClickJacking' attacks. |


### Insufficient Site Isolation Against Spectre Vulnerability  
**Risk:** Low  
**Code:** 90004  

| Affected URL | Method | Parameter | Why It Matters |
|--------------|--------|-----------|----------------|
| http://localhost:5000 | GET | Cross-Origin-Resource-Policy | Cross-Origin-Resource-Policy header is an opt-in header designed to counter side-channels attacks like Spectre. |
| http://localhost:5000/ | GET | Cross-Origin-Resource-Policy | Cross-Origin-Resource-Policy header is an opt-in header designed to counter side-channels attacks like Spectre. |
| http://localhost:5000 | GET | Cross-Origin-Embedder-Policy | Cross-Origin-Resource-Policy header is an opt-in header designed to counter side-channels attacks like Spectre. |
| http://localhost:5000/ | GET | Cross-Origin-Embedder-Policy | Cross-Origin-Resource-Policy header is an opt-in header designed to counter side-channels attacks like Spectre. |
| http://localhost:5000 | GET | Cross-Origin-Opener-Policy | Cross-Origin-Resource-Policy header is an opt-in header designed to counter side-channels attacks like Spectre. |
| http://localhost:5000/ | GET | Cross-Origin-Opener-Policy | Cross-Origin-Resource-Policy header is an opt-in header designed to counter side-channels attacks like Spectre. |


### Permissions Policy Header Not Set  
**Risk:** Low  
**Code:** 10063  

| Affected URL | Method | Why It Matters |
|--------------|--------|----------------|
| http://localhost:5000 | GET | Permissions Policy Header is an added layer of security that helps to restrict from unauthorized access or usage of browser/client features by web resources. |
| http://localhost:5000/ | GET | Permissions Policy Header is an added layer of security that helps to restrict from unauthorized access or usage of browser/client features by web resources. |
| http://localhost:5000/favicon.ico | GET | Permissions Policy Header is an added layer of security that helps to restrict from unauthorized access or usage of browser/client features by web resources. |
| http://localhost:5000/robots.txt | GET | Permissions Policy Header is an added layer of security that helps to restrict from unauthorized access or usage of browser/client features by web resources. |
| http://localhost:5000/sitemap.xml | GET | Permissions Policy Header is an added layer of security that helps to restrict from unauthorized access or usage of browser/client features by web resources. |

### Server Leaks Version Information via "Server" HTTP Response Header Field  
**Risk:** Low  
**Code:** 10036  

| Affected URL | Method | Evidence | Why It Matters |
|--------------|--------|----------|----------------|
| http://localhost:5000 | GET | Werkzeug/2.0.1 Python/3.9.25 | The web/application server is leaking version information via the "Server" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to. |
| http://localhost:5000/ | GET | Werkzeug/2.0.1 Python/3.9.25 | The web/application server is leaking version information via the "Server" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to. |
| http://localhost:5000/favicon.ico | GET | Werkzeug/2.0.1 Python/3.9.25 | The web/application server is leaking version information via the "Server" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to. |
| http://localhost:5000/robots.txt | GET | Werkzeug/2.0.1 Python/3.9.25 | The web/application server is leaking version information via the "Server" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to. |
| http://localhost:5000/sitemap.xml | GET | Werkzeug/2.0.1 Python/3.9.25 | The web/application server is leaking version information via the "Server" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to. |

### Strict-Transport-Security Header Not Set
**Risk:** Low  
**Code:** 10035
| Affected URL | Method | Why It Matters |
|--------------|--------|----------------|
| https://firefox-settings-attachments.cdn.mozilla.net/main-workspace/tracking-protection-lists/42520b78-dc12-495f-89bd-ce830a2c26c2 | GET | The application does not enforce HSTS. Without HSTS, users may be vulnerable to SSL-stripping attacks, allowing downgrade from HTTPS to HTTP. |

### Timestamp Disclosure – Unix  
**Risk:** Low  
**Code:** 10096  

| Affected URL | Method | Evidence | Why It Matters |
|--------------|--------|----------|----------------|
| https://firefox-settings-attachments.cdn.mozilla.net/… | GET | 1748394604 | The application is exposing internal timestamp data, which may allow attackers to infer system behavior, timing patterns, or operational schedules. |

### X-Content-Type-Options Header Missing  
**Risk:** Low  
**Code:** 10021  

| Affected URL | Method | Parameter | Why It Matters |
|--------------|--------|-----------|----------------|
| http://localhost:5000 | GET | x-content-type-options | Without the X-Content-Type-Options header set to 'nosniff', browsers may perform MIME-sniffing and interpret the content as a different type than declared, leading to security issues. |
| http://localhost:5000/ | GET | x-content-type-options | This issue also applies to error pages (404, 500), where browsers may still perform MIME-sniffing even when the rule does not alert. |
| https://firefox-settings-attachments.cdn.mozilla.net/... | GET | x-content-type-options | Browser sniffing may still occur on error pages, causing unintended content interpretation. |

# Scanner Comparison

## Only CodeQL (SAST) Found
- Flask debug mode enabled (debug=True), which may allow remote code execution
- Framework misconfiguration flagged through static code analysis
- CodeQL rule: py/flask-debug
- Found in: app.py:40

## Only ZAP (DAST) Found
- Content Security Policy (CSP) Header Not Set
- HTTP Only Site
- Missing Anti-clickjacking Header
- Insufficient Site Isolation Against Spectre Vulnerability
- Permissions Policy Header Not Set
- Server Leaks Version Information via "Server" HTTP Response Header Field
- X-Content-Type-Options Header Missing

## Only Dependency-Check (SCA) Found
- 0 CVEs detected
- No outdated or vulnerable packages
- No dependency advisories triggered

## All Three Tools
- None




