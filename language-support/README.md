# Language Support Matrix

Proscan SAST supports **60+ language categories** across **221 file extensions**. This matrix shows what analysis capabilities are available per language.

| Language | Regex Rules | Taint Analysis | AST Analysis | Framework Support |
|----------|-------------|----------------|--------------|-------------------|
| Java | Full | Full | Full | Spring, JAX-RS, Servlet, Struts |
| JavaScript | Full | Full | Full | Express, React, Node.js |
| TypeScript | Full | Full | Full | Express, NestJS, React |
| Python | Full | Full | Full | Django, Flask, FastAPI |
| Go | Full | Full | Full | Gin, net/http, Echo |
| C# | Full | Partial | Full | ASP.NET, .NET Core |
| PHP | Full | Full | Partial | Laravel, Symfony, WordPress |
| Ruby | Full | Full | Partial | Rails, Sinatra |
| Kotlin | Full | Partial | Partial | Spring, Android |
| Swift | Full | Partial | Partial | iOS |
| Rust | Full | Partial | Partial | — |
| Scala | Full | Partial | Partial | Play, Akka |
| C / C++ | Full | Partial | Partial | — |
| Terraform | Full | N/A | Full (HCL) | AWS, Azure, GCP |
| Kubernetes YAML | Full | N/A | Full | — |
| Dockerfile | Full | N/A | Full | — |
| CloudFormation | Full | N/A | Full | AWS |
| Helm | Full | N/A | Partial | — |
| Ansible | Full | N/A | Partial | — |
| Solidity | Full | Partial | Partial | Ethereum |
| Bash / Shell | Full | Partial | Partial | — |
| PowerShell | Full | Partial | Partial | — |
| SQL | Full | N/A | Partial | — |
| GraphQL | Full | Partial | Partial | — |
| YAML / JSON | Full | N/A | Full | — |
| ABAP | Full | N/A | N/A | SAP |
| COBOL | Full | N/A | N/A | — |
| Perl | Full | N/A | N/A | — |
| Lua | Full | N/A | N/A | — |
| R | Full | N/A | N/A | — |
| Dart | Full | Partial | N/A | Flutter |
| Elixir | Full | N/A | N/A | Phoenix |
| Erlang | Full | N/A | N/A | — |
| Haskell | Full | N/A | N/A | — |
| Groovy | Full | Partial | N/A | Grails |
| WASM | Full | N/A | N/A | — |
| Zig | Full | N/A | N/A | — |

**Legend:**
- **Full** — complete detection with all available analysis techniques
- **Partial** — rule-based detection plus limited analysis capabilities
- **N/A** — not applicable for this language/analysis type

---

## Binary Formats (Binary Analysis Scanner)

| Format | Analysis Type |
|--------|--------------|
| JVM Bytecode (.jar, .class) | Full: taint analysis, SSA, call graph, bytecode patterns |
| .NET IL (.dll, .exe) | Full: IL analysis, call graph, pattern matching |
| Android DEX (.apk, .dex) | Full: bytecode analysis, API call patterns |
| ELF (Linux) | Full: static analysis, memory safety, crypto detection |
| PE (Windows .exe, .dll) | Full: static analysis, memory safety, crypto detection |
| Mach-O (macOS) | Full: static analysis, memory safety, crypto detection |

---

## Package Ecosystems (SCA Scanner)

173 registered parsers covering:

npm, PyPI, Maven, NuGet, Go modules, RubyGems, Cargo, Composer, CocoaPods, SwiftPM, Conda, Pub (Flutter), Hex (Elixir), Conan (C/C++), vcpkg, CPAN, plus IaC package managers (Helm, Ansible Galaxy, Terraform Registry, CDK).
