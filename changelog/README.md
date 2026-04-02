# Changelog

All notable changes to Proscan are documented here.

---

## v9.0 Enterprise (Current)

### New
- Security Command Center dashboard with real-time posture across all 12 scanners
- AI/LLM Scanner with 4,600+ prompt injection techniques and OWASP LLM Top 10 coverage
- Binary & Bytecode Analysis supporting JVM, .NET IL, Android DEX, ELF, PE, and Mach-O
- Proscan Deep (Elite): 922-check dynamic scanner with 20 concurrent test groups
- Cross-scanner correlation engine with 12 XCORR rules
- Network Scanner: host discovery, port enumeration, service fingerprinting
- Remote Agents for distributed scanning
- Workflow automation engine
- Scan Comparison for trend analysis
- OWASP Benchmark v1.2 validation: 100% precision, 100% recall across all 11 CWE categories

### SAST Engine
- Interprocedural taint analysis with method-level summaries
- Constant propagation engine for dead-branch elimination
- 200,000+ detection rules across 500+ CWE categories
- 60+ language support across 221 file extensions
- CWE-330 Weak Random detection (java.util.Random, Math.random)
- CWE-501 Trust Boundary Violation detection
- CWE-327/328 Crypto detection via Cipher.getInstance and MessageDigest
- Extended path traversal sink coverage (File constructor, FileReader, FileWriter, Paths.get)
- Extended XSS sink coverage (printf, format, write, append)
- CWE-614 secure cookie detection (setSecure false)
- CWE ID population for all findings with inference fallback

### Binary Analysis
- JVM Bytecode Analyzer with SSA construction and RTA call graph
- Inter-procedural taint analysis across 41,000+ methods
- Cryptographic algorithm inventory with strength classification
- Embedded secrets detection with confidence scoring
- Hardening check against memory safety and exploit mitigation flags

### SCA
- 173 dependency parsers across 16 package ecosystems
- EPSS exploit prediction scoring integration
- CISA KEV (Known Exploited Vulnerabilities) flagging
- Reachability analysis to downgrade non-callable dependency risk

### Infrastructure
- PostgreSQL finding store with CWE and OWASP column persistence
- SARIF 2.1 export for GitHub and GitLab Security dashboards
- CycloneDX SBOM export
- WebSocket real-time scan progress broadcasting
- Adaptive scan concurrency based on target size
- Per-file finding limits to prevent noise on large codebases

---

## v8.x

### SAST
- Native rule engine with 200K+ compiled rules
- Multi-layer false positive suppression pipeline (11 stages)
- 7-factor confidence scoring model
- Advanced taint engine with Spring annotation pre-population
- Direct injection detector with variable tracking
- FP Eliminator with test file and dead code detection
- Dynamic severity adjustment

### DAST
- Enterprise checks: 100 checks across 7 categories
- CVE-specific detection layer (33 CVEs)
- Passive scanner: security headers, cookies, CORS, SSL/TLS
- Advanced scanner: 9 category functions

### Platform
- 12 scanner modules unified under single launcher
- Compliance mapping: OWASP Top 10, PCI DSS 4.0, NIST 800-53, HIPAA, SOC 2, ISO 27001, GDPR
- 6 report formats: HTML, PDF, JSON, CSV, SARIF, XML
- 6 report styles: Comprehensive, Executive, Pentest, Compliance, JSON, DAST
- IDE plugins: VS Code, JetBrains, Eclipse
- CI/CD integrations: GitHub Actions, GitLab CI, Jenkins, Azure Pipelines, CircleCI

---

## Continuous Improvement

Proscan is under active development. Improvements are released continuously based on:

- Detection quality improvements from benchmark validation
- New vulnerability patterns and CVE coverage
- Community and customer feature requests
- Performance and accuracy improvements

Contact [contact@proscan.one](mailto:contact@proscan.one) to suggest features or report issues.
