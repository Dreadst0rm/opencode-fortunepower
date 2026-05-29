---
name: secure
description: Analyze code for security vulnerabilities and enforce secure-by-default patterns
license: MIT
compatibility: opencode
metadata:
  stage: review
---

# Security Review

## When to use
- "security review", "vulnerability", "owasp"
- Any change touching: authentication, authorization, secrets, encryption
- Any change handling: user input, file uploads, SQL queries, command execution
- "CVE", "XSS", "SQLi", "CSRF", "SSRF", "RCE", "path traversal"

## Workflow
1. **Scope the review** — identify what data flows through the change
2. **Check input validation**: are all external inputs validated, sanitized, and typed?
3. **Check output encoding**: is data properly escaped for its context (HTML, SQL, shell, JSON)?
4. **Check authentication/authorization**: are protected endpoints properly gated?
5. **Check secrets**: are any credentials, tokens, or keys hardcoded?
6. **Check dependencies**: any known vulnerable dependencies?
7. **Check file operations**: path traversal, symlink attacks, temp file safety
8. **Report findings** with severity: critical / high / medium / low / info

## Common vulnerability patterns
- **Injection**: SQL, NoSQL, command, LDAP — use parameterized queries, avoid shell execution with concatenation
- **Broken auth**: weak password rules, missing rate limits, session fixation
- **Sensitive data exposure**: secrets in logs, insufficient TLS, weak encryption
- **XXE**: disable external entity processing in XML parsers
- **Broken access control**: missing ownership checks, IDOR
- **Security misconfiguration**: debug mode enabled, default credentials, unnecessary features enabled

## Language-specific notes
- **Python**: prefer `defusedxml` over `xml.etree`; use parameterized queries with SQLAlchemy/psycopg
- **JavaScript/TypeScript**: use `helmet` for Express; validate with Zod/Joi; avoid `eval()` and `innerHTML`
- **Go**: use `database/sql` parameterized queries; avoid `ioutil.ReadAll` on untrusted input

## Verification
- No hardcoded secrets
- All inputs are validated
- All outputs are properly encoded
- Dependencies are up-to-date with no known CVEs
