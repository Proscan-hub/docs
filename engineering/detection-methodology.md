# Detection Methodology

This document describes the detection strategies Proscan uses across its scanner modules.

---

## Detection Method Taxonomy

| Method | Scanner(s) | Description |
|--------|-----------|-------------|
| Pattern/Rule Matching | SAST, Secrets, IaC | Compiled patterns tested against source code |
| AST Analysis | SAST | Language-specific structural analysis |
| Taint Propagation | SAST | Source-to-sink data flow tracking |
| Direct Injection Detection | SAST | Co-occurrence analysis of sources and sinks |
| Contextual Pattern Matching | SAST | Multi-line non-comment window analysis |
| Active Payload Testing | DAST, Deep | Request mutation and response analysis |
| Entropy Analysis | Secrets | Shannon entropy calculation on candidate strings |
| Dependency Graph Analysis | SCA | Manifest parsing, version resolution, CVE correlation |
| Configuration Policy Checks | IaC, Container | Resource attribute and policy evaluation |
| Bytecode Analysis | Binary | SSA construction, call graph, binary patterns |

---

## SAST Engine

Proscan's SAST engine combines multiple detection methods simultaneously on each file:

**1. Rule-based pattern matching** — 200,000+ compiled rules across 420 rule sets. Each rule targets a specific vulnerability pattern with language binding and CWE mapping.

**2. Taint analysis** — Tracks how user-controlled data (sources) flows to security-sensitive operations (sinks). Recognizes sanitizers that break taint flows for specific vulnerability classes.

**3. Constant propagation** — Evaluates arithmetic expressions at analysis time to determine which conditional branches are always taken. Suppresses findings where the sink variable is provably constant (not user-controlled).

**4. Contextual analysis** — Multi-line pattern matching that considers the code context around each match, reducing noise from matching inside comments, string literals, or documentation.

**5. Confidence scoring** — Every finding is scored across 7 contextual factors. Findings below a calibrated threshold are eliminated without suppressing true positives.

**6. FP suppression pipeline** — Multi-stage pipeline that identifies and removes common false positive patterns while preserving all genuine vulnerabilities.

---

## DAST / Proscan Deep

Dynamic testing uses:

- **Active payload injection** — structured payloads injected into request parameters, headers, cookies, and body
- **Response differential analysis** — comparing application behavior before and after injection to identify anomalous responses
- **Out-of-band verification** — callback-based confirmation for blind injection vulnerabilities
- **Time-based detection** — timing differential analysis for SQL injection and command injection
- **Evidence-based validation** — requires response evidence (SQL error, file content, command output, script execution) before emitting a finding

---

## Secrets Detection

Dual-mode detection:

**Pattern mode** — 34 compiled regex patterns covering AWS, GCP, Azure, GitHub, Stripe, Slack, and 11 other credential types. Shannon entropy check on each match to distinguish real secrets from placeholder values.

**Entropy mode** — Parallel pass scanning for high-entropy strings above a configurable threshold (default 4.5 bits per character), minimum 20 characters.

---

## Binary Analysis

The binary scanner uses:

- **SSA construction** — Static single assignment form for precise data flow tracking
- **RTA call graph** — Rapid Type Analysis call graph for inter-procedural taint
- **Rule-based pattern matching** — 200K+ rules against disassembled binary
- **Cryptographic inventory** — Identifies cryptographic algorithms with key size and strength classification
- **Embedded string analysis** — Extracts and classifies high-entropy strings as potential secrets

---

## SCA

1. Parse manifests using 173 registered parsers
2. Resolve dependency graph (direct and transitive)
3. Batch query OSV and NVD vulnerability databases
4. Enrich with EPSS (exploit prediction) and CISA KEV (known exploited)
5. Optional reachability analysis to assess exploitability
6. Registry lookup for patch availability
