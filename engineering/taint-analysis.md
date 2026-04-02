# Taint Analysis Model

This document describes Proscan's taint analysis capabilities — what it tracks, what it detects, and its coverage scope.

---

## Analysis Scope

| Property | Value |
|----------|-------|
| Analysis type | Intra-procedural (within function boundaries) with inter-procedural method summaries |
| Source catalog | 136 registered taint sources |
| Sink catalog | 84 registered sinks |
| Sanitizer catalog | 205 registered sanitizers |
| Languages | Go, Python, JavaScript, Java, C#, Ruby, PHP, Kotlin, TypeScript, Rust, Swift |
| Vulnerability classes | 12 (see below) |

## Vulnerability Classes Tracked

| Class | Description | Primary CWE |
|-------|-------------|-------------|
| sqli | SQL injection | CWE-89 |
| cmdi | OS command injection | CWE-78 |
| xss | Cross-site scripting | CWE-79 |
| ssrf | Server-side request forgery | CWE-918 |
| path_traversal | Path/directory traversal | CWE-22 |
| redirect | Open redirect | CWE-601 |
| deserialization | Insecure deserialization | CWE-502 |
| xxe | XML external entity | CWE-611 |
| ldapi | LDAP injection | CWE-90 |
| nosqli | NoSQL injection | CWE-943 |
| ssti | Server-side template injection | CWE-94 |
| log_injection | Log injection/forging | CWE-117 |

## Source Categories

| Category | Examples |
|----------|----------|
| HTTP request parameters | getParameter, FormValue, query, params |
| HTTP request body | body, InputStream, request.body |
| HTTP headers | getHeader, headers |
| URL components | URL, Path, RequestURI |
| Cookies | getCookies, cookie |
| Form data | Form, PostForm, FILES |
| Command line | os.Args, sys.argv |
| Environment | os.Getenv, os.environ |

## Sink Categories

| Vulnerability | Sink Examples |
|---------------|--------------|
| SQL injection | db.Query, executeQuery, createQuery, prepareStatement |
| Command injection | exec.Command, Runtime.exec, os.system |
| XSS | response write methods, template output |
| SSRF | HTTP client methods, URL construction |
| Path traversal | File constructors, path operations |
| Open redirect | redirect, sendRedirect |
| XXE | XML parsers, DOM builders |
| Deserialization | readObject, pickle.loads, yaml.load |

## Framework Support

Spring/JAX-RS annotations (`@RequestParam`, `@PathVariable`, `@RequestBody`, `@RequestHeader`, `@CookieValue`, `@MatrixVariable`) are recognized as taint sources and pre-populated automatically during analysis.

## Sanitizer Recognition

The engine recognizes sanitizers by function name and vulnerability class binding. General sanitizers: `escape`, `sanitize`, `encode`, `validate`, `clean`. Language-specific sanitizers include standard library encoding functions, ESAPI methods, Apache Commons escaping, and ORM parameterization mechanisms.

## Limitations

- Analysis is intra-procedural with limited inter-procedural method summaries
- Cross-file taint tracking requires call graph construction (available for select languages)
- Framework annotation detection covers Spring/JAX-RS; other frameworks may require custom source registration
- Sanitizer recognition is name-based; custom sanitizer functions must be registered
