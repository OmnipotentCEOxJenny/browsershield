# BrowserShield

![BrowserShield logo](assets/logo.png)

BrowserShield checks a website's security setup one browser at a time. It covers security headers, HTTPS, cookies and compatibility, flags gaps and suggests fixes for Chrome, Safari, Firefox, Edge and mobile. Free and MIT-licensed, with no paid services.

## Credits
- Inventor and publisher: Rob Domaine / Omnipotent Media LLC
- Builder: Jenny Echo

## Rob Domaine's four pillars
1. Truth always: never invent; unchecked means UNVERIFIED.
2. Double-check: every finding is seen twice before it is CONFIRMED.
3. Obey laws and platform rules: only sites you own or are authorized to test; passive checks only.
4. Only legitimate, proven sources: MDN, OWASP, IETF RFCs, W3C, browser vendor docs.

## Components
- `skills/audit-browser-security`: passive audit of headers (CSP, HSTS, framing, Referrer-Policy, Permissions-Policy, COOP/COEP, nosniff), HTTPS and TLS, cookie flags, mixed content, with per-browser notes.
- `skills/write-fix-snippets`: nginx, Apache, Caddy, Netlify, Vercel and Express snippets.
- `rules/pillars-and-scope.mdc`: authorization, passive-only scope and the pillars.
- `examples/sample-report.md`: a real run on our own GitHub repo page.

## Requirements
curl and openssl. No paid APIs, no Google or Facebook services.

## Installation
Copy to `~/.cursor/plugins/local/browsershield/`, or install from the marketplace once listed.

## Feedback and reviews
- Reviews and feedback: [Discussions](https://github.com/OmnipotentCEOxJenny/browsershield/discussions)
- [Report a wrong finding](https://github.com/OmnipotentCEOxJenny/browsershield/issues/new?template=wrong-finding.md)
- [Feature request](https://github.com/OmnipotentCEOxJenny/browsershield/issues/new?template=feature-request.md)

License: MIT.
