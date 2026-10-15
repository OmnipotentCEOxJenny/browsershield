# BrowserShield report: github.com/OmnipotentCEOxJenny/course-correction (our own public repo page)
Checked: 2026-10-14, about 11:06 PM ET  Authorization: our own repo page, public, passive only  Method: two `curl -sSI` fetches, one `openssl s_client`

| # | Area | Finding | Severity | Fetch 1 | Fetch 2 | Status | Browsers affected | Fix |
|---|------|---------|----------|---------|---------|--------|-------------------|-----|
| 1 | HSTS | `max-age=31536000; includeSubdomains; preload` | pass | seen | seen | CONFIRMED | all | none |
| 2 | TLS | TLS 1.3 negotiated | pass | openssl | curl HTTP/2 over TLS | CONFIRMED | all | none |
| 3 | Framing | `X-Frame-Options: deny` plus CSP `frame-ancestors 'none'` | pass | seen | seen | CONFIRMED | all | none |
| 4 | CSP | Present, `default-src 'none'`, includes `upgrade-insecure-requests` | pass | seen | seen | CONFIRMED | all | none |
| 5 | X-Content-Type-Options | `nosniff` | pass | seen | seen | CONFIRMED | all | none |
| 6 | Cookies | `_gh_sess` and `logged_in`: HttpOnly, Secure, SameSite=Lax. `_octo`: Secure, SameSite=Lax, no HttpOnly (a tracking ID, not a session cookie) | info | seen | seen | CONFIRMED | all | none needed |
| 7 | Referrer-Policy | `no-referrer-when-downgrade`, looser than the common `strict-origin-when-cross-origin` baseline (full URL sent cross-origin over HTTPS) | low | seen | seen | CONFIRMED | all | `Referrer-Policy: strict-origin-when-cross-origin` |
| 8 | Permissions-Policy | Header not sent | low | absent | absent | CONFIRMED | Chromium browsers mainly (verify current support on MDN) | `Permissions-Policy: camera=(), microphone=(), geolocation=()` |
| 9 | COOP / COEP | Not checked in this run | | | | UNVERIFIED | | |
| 10 | HTTP to HTTPS redirect | Port 80 unreachable from the test machine (timed out) | | | | UNVERIFIED (network limit, not a site failure) | | |
| 11 | Mixed content | Not checked in this run | | | | UNVERIFIED | | |

Cookie values were redacted and never stored.

## Config snippets (for a site you control)
nginx:
```
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
add_header Permissions-Policy "camera=(), microphone=(), geolocation=()" always;
```

## Control: example.com
One fetch: HTTP/2 200 via Cloudflare with none of the security headers above (no HSTS, CSP, framing, nosniff or Referrer-Policy). SINGLE-CHECK, shown only as a contrast.
