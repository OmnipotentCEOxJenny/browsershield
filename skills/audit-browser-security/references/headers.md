# Header checklist (verify current details on the cited source)

| Header | Good baseline | Source |
|---|---|---|
| Strict-Transport-Security | `max-age=31536000; includeSubDomains` (add `preload` only when ready for the preload list) | RFC 6797; MDN; OWASP |
| Content-Security-Policy | Restrictive `default-src`, no `'unsafe-inline'` scripts, `frame-ancestors`, `base-uri`, `object-src 'none'` | W3C CSP; MDN; OWASP CSP Cheat Sheet |
| X-Frame-Options / frame-ancestors | `frame-ancestors 'none'` or `'self'`; keep `X-Frame-Options: DENY` for older browsers. MDN notes frame-ancestors supersedes X-Frame-Options | MDN |
| Referrer-Policy | `strict-origin-when-cross-origin` or stricter | W3C Referrer Policy; MDN |
| Permissions-Policy | Disable unused features, e.g. `camera=(), microphone=(), geolocation=()`. Support differs a lot by browser: check MDN compat tables | W3C; MDN |
| Cross-Origin-Opener-Policy | `same-origin` where popups across origins are not needed | HTML spec; MDN |
| Cross-Origin-Embedder-Policy | `require-corp` only if cross-origin isolation is needed; can break third-party embeds | HTML spec; MDN |
| X-Content-Type-Options | `nosniff` | Fetch spec; MDN |
| Cookies | `Secure; HttpOnly; SameSite=Lax` (or Strict); `SameSite=None` requires `Secure` | RFC 6265 and its bis draft; MDN |
