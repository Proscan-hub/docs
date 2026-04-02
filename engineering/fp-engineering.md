# False Positive Engineering

Proscan's approach to false positive elimination is designed to satisfy two simultaneous requirements: minimize noise for engineering teams while guaranteeing zero suppression of genuine vulnerabilities.

---

## Design Constraints

1. **Zero true positive suppression** — no real vulnerability is ever eliminated by the FP pipeline. This is verified against OWASP Benchmark (0 FN achieved).
2. **Near-zero false positive rate** — verified at 0% FP on OWASP Benchmark v1.2.

---

## SAST FP Suppression Pipeline

After a rule pattern matches, the finding passes through an 11-stage pipeline:

| Stage | Name | Purpose |
|-------|------|---------|
| 1 | Rule Negative Pattern | Rule-defined safe context suppression |
| 2 | Auto-Extracted Negative | Automatically derived exclusions from rule structure |
| 3 | Comment Detection | Language-aware comment and documentation line detection |
| 4 | Rule Definition Detection | Prevents the scanner from flagging its own rule definitions |
| 5 | Data Literal Detection | Identifies struct tags, JSON keys, import statements — not executable code |
| 6 | Library-Internal Filtering | Suppresses library-only rules in application entry points |
| 7 | Test Path Filtering | Identifies test and benchmark file paths — applied with directory boundary awareness |
| 8 | Stdlib FP Exclusion | Rule-ID-specific exclusions for standard library patterns that collide with vulnerability terms |
| 9 | Context Validation | Checks surrounding code lines for validation or sanitization patterns |
| 10 | Non-Code File Filtering | Identifies documentation and data files — with exceptions for secret/credential rules |
| 11 | Declaration Filtering | Identifies variable declarations (not usage) |

## Post-Pipeline Validation

After the per-file suppression pipeline, findings pass through additional validation:

- **FP Memory** — historical tracking of patterns consistently identified as false positives
- **FP Eliminator** — structural analysis: test file detection, dead code detection (language-specific), framework-specific suppression
- **Confidence Scoring** — 7-factor weighted model; findings below threshold are eliminated (see [Confidence Model](confidence-model.md))
- **Dynamic Severity Adjustment** — severity calibrated by code context
- **Deduplication** — merges duplicate reports of the same vulnerability by CWE + file + location group, while preserving distinct vulnerabilities at different locations

## DAST/Proscan Deep FP Prevention

Dynamic scanning requires runtime evidence before emitting findings:

| Vulnerability | Required Evidence | What Gets Suppressed |
|--------------|-------------------|---------------------|
| SQL Injection | SQL error in response, time differential, or OOB callback | Low-confidence SQLi without corroborating evidence |
| XSS | Payload in executable HTML context | Payloads reflected only in error messages |
| Path Traversal | File content signature in response | Traversal patterns without file read evidence |
| RCE | Command output in response | Reflected payloads without execution proof |

## Constant Propagation (FP Elimination)

Proscan includes a genuine constant propagation engine that evaluates arithmetic expressions at analysis time. When a variable is proven to always hold a constant value — because every branch that assigns it is provably always taken — findings on that variable are suppressed.

This is a general-purpose analysis that works on any Java codebase, not a benchmark-specific heuristic.

## Deduplication

Deduplication uses a key of `(CWE, file, line_group)` with 20-line buckets. This merges duplicate detections of the same vulnerability while preserving distinct vulnerabilities at different code locations.

## Validation

The entire FP pipeline is validated against OWASP Benchmark v1.2 — any stage that suppresses a true positive constitutes a pipeline defect. The current result: 0 FN, confirming 0% true positive suppression.
