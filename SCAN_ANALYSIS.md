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
| Insufficient Site Isolation Against Spectre Vulnerability | 90004 | 6 |
| Permissions Policy Header Not Set | 10063 | 5 |
| Server Leaks Version Information via "Server" HTTP Response Header Field | 10036 | 5 |
| Strict-Transport-Security Header Not Set | 10035 | 1 |
| Timestamp Disclosure - Unix | 10096 | 1 |
| X-Content-Type-Options Header Missing | 10021 | 3 |


## SCA Results (Dependency Check)
- High severity: X
- Medium severity: Y
- Low severity: Z

### Vulnerable Packages
[List packages with CVEs]

## SAST Results (CodeQL)
- Total issues: X
- By type: [breakdown]

## Recommendations
[Based on findings, what should be prioritized?]0