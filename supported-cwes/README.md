# Supported CWE Catalog

Proscan detects vulnerabilities mapped to **500+ CWE categories** across all scanner modules. This catalog lists the primary CWEs covered by each scanner.

---

## SAST (Source Code Analysis)

### Injection

| CWE | Vulnerability |
|-----|--------------|
| CWE-89 | SQL Injection |
| CWE-78 | OS Command Injection |
| CWE-79 | Cross-Site Scripting (XSS) |
| CWE-90 | LDAP Injection |
| CWE-91 | XML Injection |
| CWE-94 | Code Injection / Template Injection (SSTI) |
| CWE-98 | PHP Remote File Inclusion |
| CWE-113 | HTTP Response Splitting |
| CWE-564 | HQL Injection |
| CWE-643 | XPath Injection |
| CWE-943 | NoSQL Injection |

### Path and File

| CWE | Vulnerability |
|-----|--------------|
| CWE-22 | Path Traversal / Directory Traversal |
| CWE-23 | Relative Path Traversal |
| CWE-434 | Unrestricted File Upload |

### Authentication and Session

| CWE | Vulnerability |
|-----|--------------|
| CWE-287 | Improper Authentication |
| CWE-306 | Missing Authentication for Critical Function |
| CWE-352 | Cross-Site Request Forgery (CSRF) |
| CWE-501 | Trust Boundary Violation |
| CWE-614 | Insecure Cookie (Missing Secure Flag) |

### Cryptography

| CWE | Vulnerability |
|-----|--------------|
| CWE-295 | Improper Certificate Validation |
| CWE-310 | Cryptographic Issues |
| CWE-321 | Hardcoded Cryptographic Key |
| CWE-326 | Inadequate Encryption Strength |
| CWE-327 | Use of Broken/Risky Cryptographic Algorithm |
| CWE-328 | Reversible One-Way Hash (Weak Hash) |
| CWE-329 | Not Using a Random IV for CBC Mode |
| CWE-330 | Insufficient Entropy / Weak Random |
| CWE-338 | Use of Cryptographically Weak PRNG |

### Request Forgery and Redirect

| CWE | Vulnerability |
|-----|--------------|
| CWE-601 | Open Redirect |
| CWE-918 | Server-Side Request Forgery (SSRF) |

### Data Exposure

| CWE | Vulnerability |
|-----|--------------|
| CWE-117 | Log Injection |
| CWE-200 | Information Exposure |
| CWE-209 | Error Message Information Exposure |
| CWE-532 | Sensitive Information in Log |
| CWE-540 | Source Code Exposure |

### Deserialization

| CWE | Vulnerability |
|-----|--------------|
| CWE-502 | Deserialization of Untrusted Data |

### XML

| CWE | Vulnerability |
|-----|--------------|
| CWE-611 | XML External Entity (XXE) |
| CWE-776 | Improper Restriction of Recursive Entity References (Billion Laughs) |

### Credentials

| CWE | Vulnerability |
|-----|--------------|
| CWE-259 | Hardcoded Password |
| CWE-798 | Hardcoded Credentials |

### Other

| CWE | Vulnerability |
|-----|--------------|
| CWE-74 | Injection (General) |
| CWE-362 | Race Condition |
| CWE-444 | HTTP Request Smuggling |
| CWE-489 | Debug Mode Active |
| CWE-639 | Insecure Direct Object Reference (IDOR) |
| CWE-693 | Protection Mechanism Failure |
| CWE-942 | Permissive CORS |
| CWE-1021 | Clickjacking |
| CWE-1333 | ReDoS (Regular Expression Denial of Service) |

---

## Proscan Deep (Dynamic)

All SAST CWEs above are also tested dynamically, plus:

| CWE | Vulnerability |
|-----|--------------|
| CWE-235 | HTTP Parameter Pollution |
| CWE-284 | Authorization Bypass |
| CWE-350 | Reliance on Reverse DNS Resolution (IP Spoofing) |
| CWE-434 | File Upload |
| CWE-489 | Active Debug Code |
| CWE-639 | IDOR |
| CWE-644 | Improper Neutralization of HTTP Headers |
| CWE-1021 | Clickjacking |

---

## Secrets Detection

| CWE | Credential Type |
|-----|----------------|
| CWE-798 | Hardcoded Credentials (17 types: AWS, GCP, Azure, GitHub, Stripe, Slack, SendGrid, Twilio, Mailchimp, Heroku, JWT, private keys, database URIs, and more) |
| CWE-312 | Cleartext Storage of Sensitive Information |

---

## IaC (Infrastructure as Code)

| CWE | Vulnerability Category |
|-----|----------------------|
| CWE-16 | Configuration |
| CWE-200 | Exposed Sensitive Data |
| CWE-269 | Improper Privilege Management |
| CWE-284 | Improper Access Control |
| CWE-295 | Certificate Validation |
| CWE-732 | Incorrect Permission Assignment |

Covers: Terraform (AWS, Azure, GCP), Kubernetes, Dockerfile, CloudFormation, Helm, Ansible.

---

## Container Security

Aligned to CIS Docker Benchmark. Primary CWEs:

| CWE | Vulnerability |
|-----|--------------|
| CWE-250 | Execution with Unnecessary Privileges |
| CWE-269 | Improper Privilege Management |
| CWE-284 | Improper Access Control |
| CWE-693 | Protection Mechanism Failure |

---

## Binary Analysis

| CWE | Vulnerability |
|-----|--------------|
| CWE-119 | Buffer Errors |
| CWE-120 | Buffer Overflow (strcpy/gets) |
| CWE-122 | Heap Buffer Overflow |
| CWE-190 | Integer Overflow |
| CWE-22 | Path Traversal |
| CWE-327 | Weak Crypto in Binary |
| CWE-338 | Weak PRNG |
| CWE-415 | Double Free |
| CWE-416 | Use After Free |
| CWE-78 | Command Injection |
| CWE-787 | Out-of-Bounds Write |

---

## SCA (Software Composition Analysis)

CWE detection through CVE-to-CWE mapping via OSV, NVD, EPSS, and CISA KEV databases. Covers all CWEs present in publicly disclosed CVEs for 16 package ecosystems.

---

## AI/LLM Security

| Category | Coverage |
|---------|---------|
| OWASP LLM Top 10 | LLM01–LLM10 (full coverage) |
| Prompt Injection | CWE-74, CWE-94 equivalents |
| Data Exfiltration | CWE-200 equivalents |
| Insecure Output Handling | CWE-79 equivalents |

4,600+ techniques across 50+ subcategories.
