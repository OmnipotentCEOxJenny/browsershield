---
name: audit-browser-security
description: Passive website security-header and HTTPS check. Use whenever a user asks to check, audit or harden a site's security headers, CSP, HSTS, cookies, HTTPS redirect, mixed content or browser compatibility of those settings, for a site they own or are authorized to test. Reports gaps per browser with fixes.
---

# Audit browser security

Follow `rules/pillars-and-scope.mdc`. Required.

## Workflow
1. **Authorization gate.** Confirm the user owns or may test the site. Passive checks only.
2. **Fetch twice.** `curl -sSI https://SITE/` two times (and once more with a mobile User-Agent). Record time and status.
3. **HTTPS.** `curl -sS -o /dev/null -m 10 -w '%{http_code} %{redirect_url}' http://SITE/`: expect 301 or 308 straight to `https://` on the same host (also test `http://www.SITE/`). Do not follow redirects off-site. `openssl s_client -connect SITE:443 -servername SITE`: record protocol (TLS 1.2+ expected). If port 80 cannot be reached, mark UNVERIFIED, not failed.
4. **Headers.** Check each against `references/headers.md`: Content-Security-Policy, Strict-Transport-Security, X-Frame-Options and CSP frame-ancestors, Referrer-Policy, Permissions-Policy, Cross-Origin-Opener-Policy, Cross-Origin-Embedder-Policy, X-Content-Type-Options, Cross-Origin-Resource-Policy. CSP: flag `'unsafe-inline'` and `'unsafe-eval'` in script-src (or default-src) as medium; a `Content-Security-Policy-Report-Only` header alone enforces nothing (report it as info, not a pass). Warn on deprecated headers: X-XSS-Protection (recommend removing or `0`), Expect-CT, Public-Key-Pins (HPKP).
5. **Cookies.** For each Set-Cookie: Secure, HttpOnly (for session cookies), SameSite. Record names and flags only; redact values before saving any output, and never store raw headers containing cookies.
6. **Mixed content.** `curl -sS https://SITE/ | grep -oE '(src|href)="http://[^"]+'` on the page HTML. Flag active content (scripts, iframes, stylesheets) as high and passive content (images, media) as low. Also check `<script src>` and stylesheet links to other origins for `integrity=` (Subresource Integrity); missing SRI on third-party scripts is medium.
6b. **security.txt.** `curl -sSI https://SITE/.well-known/security.txt`: present with Contact and Expires per RFC 9116, else low.
7. **Per-browser notes.** For each header, note support differences from MDN browser-compat-data (Chrome, Edge, Firefox, Safari, Chrome Android, Safari iOS). Cite the MDN page; if not checked now, say "verify current support on MDN".
8. **Double-check.** A finding is CONFIRMED only if both fetches agree. Otherwise SINGLE-CHECK.
9. **Edge cases.** Redirect chains: audit the final same-site URL and list each hop. CDN or WAF blocks (403, 429, challenge pages): stop, report UNVERIFIED, never retry aggressively or evade. Different headers on different paths: check the home page plus one key page the user names. Rate: a few requests total.
10. **Severity.** high = exploitable gap on a sensitive page (no HTTPS, active mixed content, session cookie without Secure or HttpOnly, no CSP or framing protection on a login page); medium = weak policy (unsafe-inline, short HSTS, missing SRI); low = hardening (Permissions-Policy, Referrer-Policy, security.txt); info = notes; pass = meets the baseline (use in the report for checks that passed).
11. **Export.** On request, output findings as JSON (id, area, finding, severity, fetch1, fetch2, status, browsers, fix) or CSV with the same columns. Never include cookie values.
12. **Report** with `references/report-template.md`: finding, severity (high, medium, low, info, pass), evidence (both fetches), affected browsers, fix, and a config snippet from the write-fix-snippets skill.
