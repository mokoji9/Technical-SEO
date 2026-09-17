# Fix Guide: Missing Baseline Security Headers (CSP, X-Frame-Options, COOP)

**Category:** Security & International

## 1. What's wrong

The server doesn't send several HTTP response headers that protect visitors from common
browser-based attacks: a Content-Security-Policy (CSP), a clickjacking defense
(`X-Frame-Options` or the CSP `frame-ancestors` directive), and a Cross-Origin-Opener-Policy
(COOP). Even where HTTPS and HSTS are already configured correctly, these are a separate,
independent layer of protection.

## 2. Why it matters

- **No CSP** means that if an attacker ever manages to inject a script into the page (e.g. through
  a compromised third-party widget or a form field vulnerability), the browser has no policy
  telling it to block that script from running — a working CSP is one of the most effective
  defenses against cross-site scripting (XSS).
- **No clickjacking defense** means the page can be loaded inside an invisible `<iframe>` on an
  attacker's site and tricked into having visitors click buttons/links they can't actually see —
  a classic phishing/fraud technique.
- **No COOP** means the page's window can be reached and manipulated by a malicious pop-up or
  cross-origin window it opens, which can be used to steal information or redirect users.
- These also factor directly into Google Lighthouse's "Best Practices" score, and increasingly
  into browser security warnings shown to visitors.

## 3. How to check it yourself

1. Run:
   ```
   curl -I https://your-domain.com/
   ```
   and look for `Content-Security-Policy`, `X-Frame-Options`, and `Cross-Origin-Opener-Policy` in
   the response headers.
2. Or use [SecurityHeaders.com](https://securityheaders.com/) — paste in the URL and it grades
   every security header present or missing.
3. In Chrome Dev Tools → Lighthouse → Best Practices, look for "Ensure CSP is effective against
   XSS attacks," "Mitigate clickjacking with XFO or CSP," and "Ensure proper origin isolation
   with COOP."

## 4. Step-by-step fix

**If the site sits behind Cloudflare** (or a similar CDN/edge proxy), the simplest path is adding
these headers at the edge, without touching application code:

1. Cloudflare dashboard → **Rules → Transform Rules → Modify Response Header** (or a Cloudflare
   Worker for more control) → add:
   ```
   X-Frame-Options: SAMEORIGIN
   Cross-Origin-Opener-Policy: same-origin
   Content-Security-Policy: default-src 'self'; script-src 'self' <list every script domain you actually use, e.g. https://www.googletagmanager.com https://connect.facebook.net ...>; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; img-src 'self' data: https:; font-src 'self' https://fonts.gstatic.com;
   ```
2. **Building the CSP's `script-src`/`img-src`/etc. allowlists is the hard part** — start in
   **Report-Only mode** first so nothing breaks in production:
   ```
   Content-Security-Policy-Report-Only: default-src 'self'; ...
   ```
   Watch the browser console (or a report-collection endpoint) for what it *would* have blocked,
   add those legitimate domains to the policy, then switch from `-Report-Only` to the enforcing
   header once it's not blocking anything real.
3. **If the site is on a CMS/site builder** without direct header control, check whether it
   exposes a "custom headers" or "security headers" setting in its hosting settings — many
   platforms (Webflow, Vercel, Netlify) support this via a project settings panel or a config
   file (e.g. `netlify.toml`, `vercel.json`) rather than server code.
4. **Strengthen HSTS** (if already present but incomplete) to include subdomains and qualify for
   browser preload lists:
   ```
   Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
   ```
   Only add `preload` once you're confident every subdomain is served over HTTPS — it's very slow
   to reverse if submitted to the [HSTS preload list](https://hstspreload.org/).

## 5. How to verify the fix worked

1. Re-run `curl -I` against the live URL and confirm all three headers now appear.
2. Re-check [SecurityHeaders.com](https://securityheaders.com/) and confirm the grade improved.
3. Re-run Lighthouse's Best Practices audit and confirm the CSP/clickjacking/COOP items now pass.
4. Load the site normally in a browser and confirm nothing is broken — check the browser console
   for any new CSP violation errors, which mean a legitimate script/style domain still needs to
   be added to the policy's allowlist.

## 6. Tools to double-check

- [SecurityHeaders.com](https://securityheaders.com/)
- Chrome Dev Tools → Console (for CSP violation errors) & Lighthouse → Best Practices
- [hstspreload.org](https://hstspreload.org/) (only once HSTS is fully rolled out)
