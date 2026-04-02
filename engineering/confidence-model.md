# Confidence Scoring Model

Every finding in Proscan is assigned a confidence score that reflects the estimated probability it represents a real vulnerability. Findings below a calibrated threshold are automatically eliminated.

---

## Overview

The confidence scorer uses **7 contextual factors** to evaluate each finding. The factors capture signal quality from multiple perspectives: the rule definition, the matched code's characteristics, historical performance data, and the file's deployment context.

## The Seven Factors

| Factor | Description |
|--------|-------------|
| Base Confidence | Derived from the rule's stated confidence level (high/medium/low) |
| Severity Boost | Higher-severity rules have lower false positive rates |
| Pattern Specificity | Measures how specific and unambiguous the matched code pattern is |
| Code Context | Path-based heuristics for vendor code, generated code, and mock/test indicators |
| Historical TP Rate | Accumulated true positive rate for this rule over previous scans |
| File Reputation | Density of findings across this file relative to historical baselines |
| Environment Factor | Deployment context: production paths get higher weight than test or example directories |

## Calibration

The weights and drop threshold were calibrated against OWASP Benchmark v1.2 and the Juliet Test Suite to maximize F1 score while maintaining 0% true positive suppression — findings that are real vulnerabilities are never eliminated by the confidence scorer.

## Score Labels

| Score Range | Label |
|-------------|-------|
| 0.9 – 1.0 | very_high |
| 0.7 – 0.89 | high |
| 0.5 – 0.69 | medium |
| 0.3 – 0.49 | low |
| below 0.3 | eliminated |
