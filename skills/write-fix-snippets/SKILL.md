---
name: write-fix-snippets
description: Write server configuration snippets (nginx, Apache, Caddy, Netlify/_headers, Vercel, Express) that fix BrowserShield findings. Use after an audit or when a user asks how to add a security header or cookie flag.
---

# Write fix snippets

1. Take each finding from the report and the user's server type. Ask if unknown; otherwise give nginx and Apache.
2. Write the smallest snippet that fixes it, for example:
   - nginx: `add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;`
   - Apache: `Header always set X-Content-Type-Options "nosniff"`
   - Caddy: `header Referrer-Policy "strict-origin-when-cross-origin"`
   - Netlify `_headers`: `/*` then an indented line `  X-Frame-Options: DENY`
   - Vercel `vercel.json`: `"headers": [{"source": "/(.*)", "headers": [{"key": "X-Content-Type-Options", "value": "nosniff"}]}]`
   - Express: `res.cookie('sid', v, { secure: true, httpOnly: true, sameSite: 'lax' })`
3. Warn about breakage risks: CSP and COEP can block third-party scripts and embeds; HSTS preload is hard to undo. Suggest `Content-Security-Policy-Report-Only` first.
4. Tell the user to re-run audit-browser-security after deploying.
Never invent directives; check them against MDN or the server's official docs.
