# Security Scanning

## Overview
This repository uses three types of security scanning:

### SAST (Static Analysis with CodeQL)
- Scans source code for vulnerabilities before it runs
- Runs on push and pull requests to the `main` / `master` branches
- Checks for:
  - Code injection vulnerabilities
  - Hardcoded secrets and sensitive data
  - Insecure configurations
  - Insecure data flow patterns
  - OWASP Top 10 vulnerabilities
- Artifacts:
  - Viewable under **GitHub → Security → Code scanning alerts** (CodeQL)

### SCA (Dependency Check)
- Scans Python packages and their versions for known CVEs (Common Vulnerabilities and Exposures)
- Runs automatically on each push and pull request to the `main` / `master` branches
- Checks for:
  - Outdated dependencies with CVEs
  - Known vulnerable packages
  - License compliance issues
- Artifacts: sca-reports

### DAST (Live Application with ZAP)
- Tests running application for vulnerabilities
- Runs on push to main branch
- Checks for: 
  - SQL injection
  - Cross-site scripting (XSS)
  - Security misconfigurations
  - Broken authentication
- Artifacts: zap-baseline-reports, zap-fullscan-reports

## Reporting Vulnerabilities
Please email security@example.com