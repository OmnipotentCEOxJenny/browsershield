# BrowserShield report: github.com/OmnipotentCEOxJenny/browsershield (our own public repo page)
Checked: 2026-10-15, about 5:32 AM ET (re-test; first run 2026-10-14)  Authorization: our own repo page, public, passive only  Method: two `curl -sSI` fetches, two page GETs, one security.txt GET; TLS from openssl on 2026-10-14

| # | Area | Finding | Severity | Fetch 1 | Fetch 2 | Status | Browsers affected | Fix |
|---|------|---------|----------|---------|---------|--------|-------------------|-----|
| 1 | HSTS | `max-age=31536000; includeSubdomains; preload` | pass | seen | seen | CONFIRMED | all | none |
| 2 | TLS | TLS 1.3 negotiated (2026-10-14) | pass | openssl | curl HTTP/2 over TLS | CONFIRMED | all | none |
| 3 | Framing | `X-Frame-Options: deny` plus CSP `frame-ancestors 'none'` | pass | seen | seen | CONFIRMED | all | none |
| 4 | CSP | Enforced (not Report-Only). `script-src github.githubassets.com` plus one sha256 hash; no `'unsafe-inline'` or `'unsafe-eval'`; `upgrade-insecure-requests` | pass | seen | seen | CONFIRMED | all | none |
| 5 | X-Content-Type-Options | `nosniff` | pass | seen | seen | CONFIRMED | all | none |
| 6 | Deprecated headers | `X-XSS-Protection: 0` (the recommended value); no Expect-CT or Public-Key-Pins | pass | seen | seen | CONFIRMED | all | none |
| 7 | Cookies (2026-10-14 run) | `_gh_sess` and `logged_in`: HttpOnly, Secure, SameSite=Lax. `_octo`: Secure, SameSite=Lax, no HttpOnly (tracking ID, not a session cookie). Values never stored | info | seen | seen | CONFIRMED | all | none needed |
| 8 | Referrer-Policy | `no-referrer-when-downgrade`, looser than the `strict-origin-when-cross-origin` baseline | low | seen | seen | CONFIRMED | all | `Referrer-Policy: strict-origin-when-cross-origin` |
| 9 | Permissions-Policy | Header not sent | low | absent | absent | CONFIRMED | MDN 2026-10-14: limited availability, not Baseline | `Permissions-Policy: camera=(), microphone=(), geolocation=()` |
| 10 | COOP / COEP / CORP | None sent on this HTML page | low | absent | absent | CONFIRMED | all | `Cross-Origin-Opener-Policy: same-origin` if cross-origin popups are not needed |
| 11 | Mixed content | 0 `src` or `href` values with `http://` | pass | 0 | 0 | CONFIRMED | all | none |
| 12 | Subresource Integrity | 9 scripts, all from `github.githubassets.com`, none with `integrity=`; that host is GitHub's own asset domain and is pinned in script-src | info | 9/0 | 9/0 | CONFIRMED | all | Optional: add SRI if the asset host is ever shared or third-party |
| 13 | security.txt | `https://github.com/.well-known/security.txt` has Contact and Expires (RFC 9116) | pass | seen | (single GET) | SINGLE-CHECK | n/a | none |
| 14 | HTTP to HTTPS redirect | Not testable: outbound port 80 is blocked from the test machine (curl timed out for github.com and example.com) | | | | UNVERIFIED (test-machine network limit, not a site failure; HSTS preload covers browsers that ship the preload list) | | |

## Config snippets (for a site you control)
nginx:
```
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
add_header Permissions-Policy "camera=(), microphone=(), geolocation=()" always;
add_header Cross-Origin-Opener-Policy "same-origin" always;
```

## Control: example.com
One fetch (2026-10-14): HTTP/2 200 via Cloudflare with none of the security headers above. SINGLE-CHECK, shown only as a contrast.
