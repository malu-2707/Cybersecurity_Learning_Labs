# Module 3 — Web Application Security

**Level:** Intermediate
**Duration:** Days 11–15
**Environment:** Kali Linux
**Status:** In Progress

## Overview

This module focuses on understanding web application security through practical command-line exercises and controlled lab testing.

The goal is to understand HTTP communication, inspect web responses, learn common web vulnerabilities, and study secure coding and remediation techniques.

## Learning Objectives

* Understand HTTP and HTTPS.
* Inspect HTTP response headers and status codes.
* Learn about cookies, sessions, authentication, and authorization.
* Study common OWASP Top 10 vulnerability categories.
* Understand injection, Cross-Site Scripting (XSS), and Broken Access Control.
* Learn secure coding and remediation practices.
* Document findings from authorized lab exercises.

## Tools and Technologies

* Kali Linux
* `curl`
* Linux networking utilities
* Burp Suite
* OWASP ZAP
* Nmap
* Browser Developer Tools

Tool availability depends on the local environment.

## Day 11 — HTTP Fundamentals

### Inspect HTTP response headers

```bash
curl -I https://example.com
```

Displays response headers from the example website.

### Check HTTP status and content type

```bash
curl -sS -o /dev/null -w 'HTTP status: %{http_code}\nContent type: %{content_type}\n' https://example.com
```

Displays the HTTP status code and response content type.

### Inspect response content

```bash
curl -sS https://example.com | head -n 15
```

Displays the first 15 lines of the response body.

### Check DNS resolution

```bash
getent hosts example.com
```

Displays the IP address resolved for the hostname.

## Day 12 — Cookies, Sessions, and Access Control

### Inspect response headers

```bash
curl -sS -D - -o /dev/null https://example.com
```

Displays the HTTP response headers.

### Inspect redirect behavior

```bash
curl -sS -I -L --max-redirs 5 https://example.com
```

Follows redirects and displays response headers.

### Key concepts

* **Cookies:** Browser-stored data associated with a website.
* **Sessions:** Maintain application state between requests.
* **Authentication:** Verifies a user's identity.
* **Authorization:** Determines which resources a user can access.
* **Secure and HttpOnly:** Cookie attributes that help protect session cookies.

## Day 13 — OWASP Vulnerabilities

The OWASP Top 10 highlights important web application security risks.

Topics covered:

* Broken Access Control
* Security Misconfiguration
* Software Supply Chain Failures
* Cryptographic Failures
* Injection
* Insecure Design
* Authentication Failures
* Software or Data Integrity Failures
* Security Logging and Alerting Failures
* Mishandling of Exceptional Conditions

### Inspect local listening services

```bash
ss -tulpn
```

Lists listening network sockets on the local machine.

### Check an HTTPS response

```bash
curl -I --max-time 5 https://example.com
```

Tests whether the example website responds to a HEAD request within the timeout.

## Day 14 — Secure Coding and Remediation

### Check installed tools

```bash
command -v curl
command -v burpsuite
command -v zaproxy
command -v nmap
```

Checks whether the corresponding commands are available.

### Secure coding practices

* Validate untrusted input.
* Use parameterized database queries.
* Encode output appropriately to reduce XSS risks.
* Enforce authorization on the server.
* Protect session cookies.
* Avoid exposing secrets in application logs.
* Keep application dependencies updated.

### Remediation workflow

1. Identify a potential vulnerability in an authorized lab.
2. Record the affected component and evidence.
3. Explain the impact.
4. Recommend and apply a fix.
5. Repeat the original test.
6. Document the verification result.

## Day 15 — Assessment and Documentation

### Inspect network interfaces

```bash
ip -br addr
```

Displays a concise summary of network interfaces and addresses.

### Inspect listening services

```bash
ss -tulpn
```

Lists listening sockets.

### Test an HTTPS response

```bash
curl -I --max-time 5 https://example.com
```

Checks the response from the example website.

### Vulnerability report template

Each confirmed finding should include:

* **Title:** Name of the vulnerability.
* **Affected component:** Page, endpoint, or feature.
* **Severity:** Based on evidence and realistic impact.
* **Description:** What the issue is and how it occurs.
* **Reproduction steps:** Authorized steps to reproduce the issue.
* **Evidence:** Relevant output or sanitized screenshots.
* **Impact:** Potential consequences.
* **Remediation:** Recommended fix.
* **Verification:** Results after the fix is applied.

## Security Guidelines

* Test only systems I own or have explicit permission to assess.
* Use a local or deliberately vulnerable training application for security testing.
* Do not expose passwords, API keys, session cookies, or other secrets.
* Keep evidence accurate and distinguish confirmed findings from assumptions.
* Verify fixes before marking vulnerabilities as resolved.

## Results and Findings

Actual command outputs, lab observations, confirmed vulnerabilities, and remediation results will be added as the practical exercises are completed.

## Conclusion

Module 3 builds practical knowledge of web application security using Kali Linux. The focus is on understanding HTTP, recognizing common vulnerabilities, testing only authorized environments, and documenting evidence-based remediation.
