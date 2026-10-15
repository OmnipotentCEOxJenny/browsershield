# Changelog

## 1.0.6 (2026-10-15)
- Merged the two pillars sections in the rule file into one, in Rob Domaine's words and order; all earlier rules kept as sub-bullets.

## 1.0.5 (2026-10-15)
- Added README "Project status: done, pending, uncertain" section.
- Pillars restated in Rob Domaine's wording in the README and rule file.

## 1.0.4 (2026-10-15)
- Full re-test. Sample report re-run with CSP unsafe-* check, deprecated headers, SRI and security.txt rows. Added "pass" to the severity scale (the sample already used it). Netlify and Vercel snippet examples added (the skill listed them without examples).

## 1.0.3 (2026-10-14)
- Per-browser notes checked against MDN (Permissions-Policy, X-Frame-Options wording fixed); sample re-run for COOP/COEP/CORP and mixed content; JSON and CSV export examples.

## 1.0.2 (2026-10-14)
- Clearer trigger description, README quick start, edge cases (redirect chains, CDN or WAF blocks, per-path headers, low request rate), severity scoring, JSON and CSV export.

## 1.0.1 (2026-10-14)
- Precise http-to-https redirect test; CORP, SRI, security.txt (RFC 9116), CSP unsafe-inline/unsafe-eval and Report-Only handling, HSTS preload eligibility, deprecated-header warnings; mixed content split active/passive.
- Legal wording (authorization, CFAA, not a pen test) and cookie-value redaction rule.

## 1.0.0 (2026-10-14)
- First release: audit-browser-security and write-fix-snippets skills, pillars rule, sample report.
