# Security Scan Analysis - [2/12/2025]

## DAST Results (ZAP Baseline)
- Total URLs scanned: 2
- PASS: Not reported in ZAP output (standard reporting format)
- WARN-NEW: 6 warnings
- FAIL-NEW: 2 failures

### Warning Summary
1. **Content Security Policy (CSP) Header Not Set** (Medium) - 2 instances
2. **Missing Anti-clickjacking Header** (Medium) - 1 instance
3. **Insufficient Site Isolation Against Spectre Vulnerability** (Low) - 3 instances
4. **Permissions Policy Header Not Set** (Low) - 3 instances
5. **Server Leaks Version Information** (Low) - 3 instances
6. **X-Content-Type-Options Header Missing** (Low) - 1 instance

## SCA Results (Dependency Check)
- High severity: 0
- Medium severity: 0
- Low severity: 0

### Vulnerable Packages
No vulnerable packages

## SAST Results (CodeQL)
- Total issues: 1
- By Severity: 1 High (Flask debug mode)
- By Type: Security Misconfiguration

## Recommendations
Flask Debug Mode Remediation
Debug mode should be disabled (debug=False)

# Scanner Comparison

## Only CodeQL (SAST) Found
- Flask debug mode enabled in production code (debug=True at app.py:40)
- Code pattern vulnerability (framework-specific security misconfiguration)
- Source code security rule violations (py/flask-debug rule triggered)

## Only ZAP (DAST) Found
- Missing security headers (6 different headers: CSP, X-Frame-Options, X-Content-Type-Options, Permissions-Policy, Cross-Origin headers)
- Runtime configuration issues (Server version leakage: Werkzeug/2.0.1 Python/3.9.25)
- HTTP protocol vulnerabilities (Missing Sec-Fetch headers: Dest, Mode, Site, User - 12 total instances)
- Cache control misconfiguration (Content cacheable for 1 year without explicit directives)
- Modern web application detection (AJAX-based application patterns)

## Only Dependency-Check (SCA) Found
- Clean dependency status (No CVEs in Python packages)
- Dependency vulnerability assessment (Validated against CVE databases)
- Transitive dependency analysis (Complete dependency tree inspection)

## All Three Tools
- (Unlikely - they focus on different layers) Each tool operates at distinct application layers (source code, runtime, dependencies) with minimal overlap