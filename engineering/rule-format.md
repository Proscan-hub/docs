# Rule Format

This document describes the structure of Proscan detection rules. The full rule database (200,000+ rules) is proprietary. This page documents the rule schema and shows the types of detections it enables.

---

## SAST Rule Schema

Each SAST rule is a structured definition with the following fields:

```
NativeRule {
  ID          string    // Unique rule identifier (e.g., "JAVA-SEC-031")
  Title       string    // Human-readable vulnerability title
  Severity    string    // ERROR, WARNING, INFO
  Confidence  string    // HIGH, MEDIUM, LOW
  Category    string    // Rule category
  CWEs        []string  // CWE identifiers (e.g., ["CWE-89"])
  OWASP       []string  // OWASP Top 10 mapping
  Pattern     regex     // Compiled positive detection pattern
  Negative    regex     // Optional: compiled safe-context suppression pattern
  Languages   []string  // File extensions this rule applies to
  Description string    // What the rule detects and why it matters
  Remediation string    // How to fix the vulnerability
  References  []string  // External references
}
```

## Design Principles

- Every rule has a **positive pattern** (what to detect) and an optional **negative pattern** (what to suppress as safe context)
- Rules are **language-bound** — they only fire on files with matching extensions
- Every rule maps to at least one **CWE identifier** for compliance traceability
- **Remediation guidance** is mandatory — all findings include fix instructions
- Rules are organized into **420 rule sets** grouped by vulnerability class, language, and detection depth

## Rule Coverage

| Category | Rules |
|----------|-------|
| Injection (SQL, command, XSS, XXE, LDAP, XPath, NoSQL, SSTI) | High density |
| Authentication and session management | High density |
| Cryptographic weaknesses | High density |
| Sensitive data exposure | High density |
| Security misconfiguration | High density |
| Vulnerable dependencies | Via SCA scanner |
| Insecure deserialization | High density |
| Path and file operations | High density |
| Network and API security | High density |
| AI/ML security | High density |

Total: 200,000+ rules, 420 rule sets, 500+ CWE categories

---

## Taint Source/Sink Schema

Taint analysis uses catalogs of sources, sinks, and sanitizers:

```
TaintSource {
  Lang     string  // Language restriction (".java", ".py", etc.) or "" for all
  Object   string  // Receiver/package name
  Member   string  // Field or method name
  IsField  bool    // true = field access, false = method call
  Label    string  // Human description
}

TaintSink {
  Lang        string    // Language restriction
  Object      string    // Receiver/package
  Function    string    // Method/function name
  ArgIdx      int       // Which argument is dangerous
  VulnClass   string    // Vulnerability category
  CWEs        []string  // CWE mappings
  Remediation string    // Fix guidance
}

TaintSanitizer {
  Lang     string  // Language restriction
  Object   string  // Package/module
  Function string  // Function name
  ForClass string  // Which vulnerability class it sanitizes
}
```

The catalog contains **136 sources**, **84 sinks**, and **205 sanitizers** across 11 languages.

---

## Secrets Pattern Schema

```
SecretPattern {
  ID          string  // Pattern identifier
  Name        string  // Human name
  Pattern     regex   // Compiled detection regex
  Severity    string  // critical, high, medium
  Type        string  // Secret category (aws, github, jwt, etc.)
  Description string  // What the pattern detects
}
```

34 patterns covering: AWS, GCP, Azure, GitHub, Stripe, Slack, SendGrid, Twilio, Mailchimp, Heroku, JWT, private keys, database credentials, passwords, and generic secrets.

---

## IaC Rule Schema

```
IaCRule {
  ID          string     // Rule identifier (e.g., "TF001")
  Name        string     // Rule name
  Description string     // What misconfiguration it detects
  Severity    string     // critical, high, medium, low
  Category    string     // Functional category
  Platform    string     // terraform, kubernetes, dockerfile, cloudformation
  Remediation string     // Fix guidance
}
```

~2,300 rules covering Terraform (AWS, Azure, GCP), Kubernetes, Dockerfile, CloudFormation, Helm, and Ansible.
