# Security Scanning

## Overview
This repository implements a comprehensive security scanning pipeline using three complementary approaches to ensure application security across different layers of the stack.

### SAST (Static Analysis with CodeQL)
- Scans source code for vulnerabilities
- Runs on push to main branch
- Checks for:

Flask debug mode in production
Hardcoded secrets and credentials
SQL injection patterns
Cross-site scripting (XSS) vulnerabilities
Insecure deserialization
Path traversal issues
Framework-specific security misconfigurations

- Artifacts: See GitHub Security tab

### SCA (Dependency Check)
- Scans Python packages for known CVEs
- Runs on push to main branch
- Checks for:

Known vulnerabilities in dependencies (CVEs)
Outdated package versions
License compliance issues
Transitive dependency vulnerabilities
Package integrity issues

- Artifacts: dependency-check-report.csv, dependency-check-report.html

### DAST (Live Application with ZAP)
- Tests running application for vulnerabilities
- Runs on push to main branch
- Checks for:

Missing security headers (CSP, X-Frame-Options, etc.)
Information disclosure (server version leakage)
Clickjacking vulnerabilities
Cross-site scripting (XSS)
SQL injection (runtime testing)
Cache control miscnfigurations
API security issues
Modern web application security

- Artifacts: zap-baseline-report.md, zap-fullscan-report.html, zap-report.json

## Understanding Results

- Severity Levels
High/Critical: Immediate action required (24-72 hours)
Medium: Address within 2 weeks
Low: Address within 1 month
Informational: Best practices, no immediate security impact

- Tool-Specific Interpretation
1. CodeQL (SAST)
Focuses on code patterns and logic errors
High confidence findings are typically accurate
False positives may occur with custom code patterns

2. Dependency-Check (SCA)
CVSS scores indicate vulnerability severity (0-10 scale)
Pay attention to exploitability metrics
Some findings may be false positives for unused code paths

3. ZAP (DAST)
Missing headers = Configuration gaps
Information leakage = Attack surface exposure
Modern web app detection = Need for additional client-side testing

## Reporting Vulnerabilities
Please email security@example.com