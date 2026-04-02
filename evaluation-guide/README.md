# How to Evaluate a SAST Tool

This guide describes how to evaluate any SAST tool rigorously, including Proscan. We publish this because we believe transparent evaluation methodology benefits the entire security community — and because we are confident Proscan performs well under rigorous testing.

---

## Why Most SAST Evaluations Are Wrong

Most organizations evaluate SAST tools by:

1. Running the tool on their codebase and counting findings
2. Spot-checking 10-20 findings manually
3. If most look real, they accept the tool

This approach has two fatal flaws:

- **High finding count does not mean high quality.** A tool that flags everything will have high recall but terrible precision. Your team will spend most of their time chasing false positives.
- **Low finding count does not mean high quality either.** A tool that is overly conservative will miss real vulnerabilities.

The correct metrics are **precision** and **recall** — and you cannot calculate them without ground truth.

---

## Step 1: Use Standardized Test Suites (Ground Truth Available)

### OWASP Benchmark v1.2 (Java)

- **Source:** [github.com/OWASP-Benchmark/BenchmarkJava](https://github.com/OWASP-Benchmark/BenchmarkJava)
- **Test cases:** 2,740 Java test cases, each labeled true positive or false positive
- **Ground truth:** `expectedresults-1.2.csv` — every test case has a known answer
- **How to use:** Run your SAST tool against the source code. For each finding, look up the test case in the CSV. Calculate TP, FP, FN, TN per CWE category.

### NIST Juliet Test Suite (Multi-language)

- **Source:** [samate.nist.gov/SARD](https://samate.nist.gov/SARD/test-suites/111)
- **Test cases:** 80,000+ test cases for C/C++ and Java
- **Ground truth:** Each test case has a documented CWE and a known vulnerable/safe variant

### Deliberately Vulnerable Applications (Runtime Validation)

For DAST validation: WebGoat, DVWA, Juice Shop, NodeGoat. These are not ground-truth complete but are useful for qualitative verification.

---

## Step 2: Calculate the Right Metrics

```
True Positive (TP)  = scanner correctly identified a real vulnerability
False Positive (FP) = scanner flagged safe code as vulnerable
False Negative (FN) = scanner missed a real vulnerability
True Negative (TN)  = scanner correctly stayed silent on safe code

Precision = TP / (TP + FP)   — what fraction of findings are real?
Recall    = TP / (TP + FN)   — what fraction of real vulns were found?
F1 Score  = 2 × (Precision × Recall) / (Precision + Recall)
```

**Do not evaluate by finding count alone.** Always calculate precision and recall.

---

## Step 3: Evaluate Per CWE Category

A tool might score well overall but poorly on specific vulnerability types. Always break down results by CWE category:

- A tool with 90% precision on SQL injection may have 40% precision on cryptographic issues
- Aggregate numbers hide category-level weaknesses

---

## Step 4: Evaluate on Your Own Codebase

Benchmark suites test synthetic patterns. Your real codebase has different characteristics:

- More complex data flows
- Custom frameworks and libraries
- More varied code styles

Request a demo scan on your own code. During evaluation:

1. Review a random sample of 20-30 findings for FP assessment
2. Check if known vulnerabilities in your code are detected (if you have existing CVEs or pen test findings, use those as ground truth)
3. Measure scan time on your largest repository

---

## Step 5: Ask These Questions

Before selecting any SAST tool:

1. **What is your score on OWASP Benchmark?** If they don't publish it, ask why.
2. **What is your false positive rate on real-world Java/Python/Go code?** (Benchmark tests synthetic patterns; real code is harder.)
3. **How do you handle sanitizer recognition?** Does the tool understand that HTML encoding protects XSS but not SQL injection?
4. **Can I see the findings on a deliberately vulnerable app?** Run the tool against WebGoat or DVWA and check if it finds the known vulnerabilities.
5. **What happens when I mark a finding as false positive?** Good tools learn from triage feedback.

---

## Proscan's Results

| Benchmark | TP | FP | FN | Precision | Recall | F1 |
|-----------|----|----|-----|-----------|--------|-----|
| OWASP Benchmark v1.2 | 1,415 | 0 | 0 | 100% | 100% | 100% |

Full per-CWE breakdown: [OWASP Benchmark Scorecard](../benchmark/results/OWASP_BENCHMARK_SCORECARD.md)

To evaluate Proscan on your own codebase: [contact@proscan.one](mailto:contact@proscan.one)
