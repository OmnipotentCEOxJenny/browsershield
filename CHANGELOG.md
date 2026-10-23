# Changelog

## 1.0.15 (2026-10-23)
- Remove internal notes from the README, translations, rule file (renamed to `rules/scope.mdc` where applicable) and skills. Local tests re-run and passed. Not tested in-app. Not submitted to the marketplace.

## 1.0.14 (2026-10-23)
- README: new "Testing status" section. Local automated tests pass; in-app testing is not yet completed. Records that the marketplace submit form's "tested locally and in-app" confirmation (2026-10-14) was checked in error before any in-app test; in-app testing is pending.
- Docs only; no behavior changes. Local tests re-run and passed. Not tested in-app. Not resubmitted.

## 1.0.13 (2026-10-23)
- Translations: each language section in TRANSLATIONS.md now starts with a one-line notice in that language saying it is a machine translation, not reviewed by a native speaker, and that the English version is authoritative. README Languages section notes this. No behavior changes.
- Local tests re-run and passed. Not tested in-app. Not submitted to the marketplace.

## 1.0.12 (2026-10-23)
- Search keywords: 36 to 40 (added SameSite, CertificateExpiry, SecurityTxt, HttpsRedirect), all BrowserShield-specific, per Rob's keyword rules.
- Local tests re-run and passed. Not tested in-app. Not submitted to the marketplace.

## 1.0.11 (2026-10-22)
- Logo resized from 512x512 to 1024x1024 to match the rest of the plugin set (same artwork, no visual change). No behavior changes.

## 1.0.10 (2026-10-21)
- Added `tests/check_frontmatter.py`: a strict YAML front-matter check (PyYAML `safe_load`) for every SKILL.md and rules .mdc file, plus a plugin.json JSON check. Run `python3 tests/check_frontmatter.py` from the repo root; it catches the unquoted-colon bug fixed in PluginPulse 1.0.2.
- No behavior changes to skills or rules.

## 1.0.9 (2026-10-20)
- TRANSLATIONS.md: each of the 23 languages now includes this plugin's specific limits list (from the README's "Honest assessment: what this plugin cannot do" section) plus the marketplace status. Machine translations, not reviewed by native speakers.
- Docs only; no behavior changes.

## 1.0.8 (2026-10-20)
- README follows the shared template: title, plain description, logo, existing content, and a new final section "Honest assessment: what this plugin cannot do" listing real limits and the compliance statement.
- TRANSLATIONS.md now covers the same 23 languages as every Omnipotent plugin (title, description and honest-assessment summary for each), all marked as machine translations not reviewed by native speakers.
- Docs only; no behavior changes.

## 1.0.7 (2026-10-20)
- Fix: the documented `openssl s_client` command waited for input and hung; it now ends with `</dev/null`.
- Fix: the mixed-content grep missed single-quoted and unquoted `src`/`href` attributes; it now catches all three (tested).
- Multi-language: the rule file and both skills tell the AI to answer in the user's language and keep commands, header names and status labels unchanged. Added TRANSLATIONS.md with short summaries in 20 languages (machine-made, not yet reviewed by a native speaker).
- Requirements list the tested curl (8.14.1) and OpenSSL (3.5.7) versions. "No Google or Facebook services" reworded to "No Google or Facebook account is required".

## 1.0.6 (2026-10-15)
- Docs wording edit.

## 1.0.5 (2026-10-15)
- Added README "Project status: done, pending, uncertain" section.

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
- First release: audit-browser-security and write-fix-snippets skills, sample report.
