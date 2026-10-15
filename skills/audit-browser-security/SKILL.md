---
name: audit-browser-security
description: Passively audit a website the user owns or is authorized to test for security headers, HTTPS and TLS, cookie flags and mixed content, and report support differences per browser (Chrome, Safari, Firefox, Edge, mobile) with fixes. Use when a user asks to check a site's browser security setup.
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
9. **Report** with `references/report-template.md`: finding, severity (high, medium, low, info), evidence (both fetches), affected browsers, fix, and a config snippet from the write-fix-snippets skill.
