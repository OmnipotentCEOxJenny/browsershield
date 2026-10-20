# BrowserShield

BrowserShield checks a website's security setup one browser at a time. It covers security headers, HTTPS, cookies and compatibility, flags gaps and suggests fixes for Chrome, Safari, Firefox, Edge and mobile. Free and MIT-licensed, with no paid services.

![BrowserShield logo](assets/logo.png)

## Project status: done, pending, uncertain
**Done**
- 2026-10-20: v1.0.7 fixes a hanging openssl command and a mixed-content grep that missed single-quoted and unquoted links; adds multi-language answers and 20 translated summaries (machine-made, not yet native-reviewed); full re-test PASS.
- 2026-10-15: v1.0.6 merges the pillars into one section in Rob's words (rule file and README).
- 2026-10-15: full re-test PASS (manifest, frontmatter, file links, JSON/CSV export columns, two-fetch passive audit of our own repo page).
- 2026-10-14: per-browser notes for Permissions-Policy and X-Frame-Options checked against MDN.

**Pending**
- The plain-http to https redirect check was never verified, because port 80 is blocked from the build machine. It needs a test from a network where port 80 is reachable.
- Per-browser notes were checked against MDN for only two headers; the rest are pending.
- security.txt row in the sample is SINGLE-CHECK (one fetch).
- Marketplace review: submitted 2026-10-14, pending, no approval yet.

**Uncertain**
- How the listing works on the Grok Bot and Grok side: not described in the Cursor publisher terms, so not confirmed.
- Whether xAI review will require changes: unknown until review.

## Quick start
1. Install (see Installation).
2. Ask: "Run BrowserShield on https://your-site.example" (a site you own or may test).
3. Get a findings table with two checks each, per-browser notes, server snippets, and optional JSON or CSV export.

## Credits
- Inventor and publisher: Rob Domaine / Omnipotent Media LLC
- Builder: Jenny Echo

## Rob Domaine's four pillars
1. Trustworthy, honest, real data, truthful: never invent; anything unchecked is marked UNVERIFIED.
2. Use only legitimate means: legitimate, proven sources and methods; unreliable sources rejected.
3. Double-check everything: every finding is confirmed by two independent checks, and the report shows both.
4. Stay within the law and rules always: local, county, state, federal and platform rules.

## Legal and scope
Only test sites you own or have written permission to test. Unauthorized testing can violate laws such as the U.S. CFAA. BrowserShield is a passive configuration review, not a penetration test, and never stores cookie values. Not legal advice.

## Components
- `skills/audit-browser-security`: passive audit of headers (CSP, HSTS, framing, Referrer-Policy, Permissions-Policy, COOP/COEP, nosniff), HTTPS and TLS, cookie flags, mixed content, with per-browser notes.
- `skills/write-fix-snippets`: nginx, Apache, Caddy, Netlify, Vercel and Express snippets.
- `rules/pillars-and-scope.mdc`: authorization, passive-only scope and the pillars.
- `examples/sample-report.md`: a real run on our own GitHub repo page.

## Requirements
curl and openssl (tested with curl 8.14.1 and OpenSSL 3.5.7; any current release should work). No paid APIs. No Google or Facebook account is required.

## Installation
Copy to `~/.cursor/plugins/local/browsershield/`, or install from the marketplace once listed.

## Languages
The AI answers in the user's language and keeps commands, file names and status labels unchanged. Title, description and honest-assessment summaries in 23 languages are in [TRANSLATIONS.md](TRANSLATIONS.md): Español, Français, Português, Deutsch, Italiano, Nederlands, Polski, Русский, Українська, Türkçe, العربية, עברית, فارسی, हिन्दी, বাংলা, اردو, 简体中文, 日本語, 한국어, Bahasa Indonesia, Tiếng Việt, Kiswahili, Tagalog / Filipino. They are machine translations, not yet reviewed by native speakers; the English text is authoritative.

## Feedback and reviews
- Reviews and feedback: [Discussions](https://github.com/OmnipotentCEOxJenny/browsershield/discussions)
- [Report a wrong finding](https://github.com/OmnipotentCEOxJenny/browsershield/issues/new?template=wrong-finding.md)
- [Feature request](https://github.com/OmnipotentCEOxJenny/browsershield/issues/new?template=feature-request.md)

License: MIT.

## Honest assessment: what this plugin cannot do
Written to be fully transparent. If something here is wrong or out of date, please open an issue.

- It runs passive checks only (headers, HTTPS, cookies, compatibility). It is not a penetration test or vulnerability scanner and does not attack or exploit anything.
- Use it only on sites you own or are authorized to test.
- A clean report does not mean a site is secure; results reflect only the moment of the check.
- The HTTP-to-HTTPS redirect check has not yet been re-tested end to end (it needs port 80).
- Per-browser notes are based on MDN and change as browsers update.
- It needs curl and OpenSSL on your computer (tested: curl 8.14.1, OpenSSL 3.5.7).
- Marketplace: submitted and still pending review; it is not an approved listing yet.
- Translations: the 23 translated summaries in [TRANSLATIONS.md](TRANSLATIONS.md) are machine-made and have not been reviewed by native speakers. The English text is authoritative.
- It is not legal advice and cannot guarantee that any particular use is lawful; you remain responsible for how you use it.
- Rules and compliance: it is built to follow all local, county, state and federal laws and every platform's rules. It uses no paid services, never bypasses logins, paywalls, CAPTCHAs or access controls, and never claims a feature it does not have.
