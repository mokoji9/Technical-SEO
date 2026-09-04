# Fix Guide: Site Not Fully on HTTPS / Missing HTTP → HTTPS Redirect

**Category:** Security & Internationalization

## 1. What's wrong

The site is accessible over both HTTP and HTTPS without HTTP automatically redirecting to
HTTPS — or parts of the site load insecure (HTTP) resources on HTTPS pages ("mixed
content").

## 2. Why it matters

HTTPS is a confirmed Google ranking factor and a browser trust signal — browsers show
"Not Secure" warnings on HTTP pages, which scares off visitors. Without a proper redirect,
you can also end up with both HTTP and HTTPS versions indexed as duplicate content.

## 3. How to check it yourself

1. Visit `http://yourdomain.com` (without the `s`) — it should automatically redirect to
   `https://yourdomain.com`. If it loads without redirecting, that's the issue.
2. Check for a valid SSL certificate (padlock icon in the browser address bar).
3. Open Dev Tools → Console on an HTTPS page and look for "Mixed Content" warnings
   (resources still loading over HTTP).

## 4. Step-by-step fix

1. **Get/confirm an SSL certificate** is installed (most hosts offer free ones via Let's
   Encrypt, or check with your hosting provider).
2. **Force HTTP → HTTPS redirect** at the server level:

   Apache (`.htaccess`):
   ```
   RewriteEngine On
   RewriteCond %{HTTPS} off
   RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
   ```

   Nginx:
   ```
   server {
     listen 80;
     server_name yourdomain.com;
     return 301 https://$host$request_uri;
   }
   ```

   Many hosts/CDNs (Cloudflare, Netlify, Vercel, etc.) have a one-click "Always use HTTPS"
   toggle instead — check there first.
3. **Fix mixed content** — update any hardcoded `http://` links to images, scripts, or
   stylesheets to `https://` (or protocol-relative `//`).
4. **Update your canonical tags, sitemap, and internal links** to all use `https://` URLs.
5. Update Google Search Console to add/verify the `https://` property if not already done,
   and set it as the preferred domain.

## 5. How to verify the fix worked

1. Visit the `http://` version of a few pages — confirm they 301-redirect to `https://`.
2. Recheck Dev Tools Console for mixed content warnings — should be gone.
3. Confirm the padlock/secure icon shows on all pages.

## 6. Tools to double-check

- Browser address bar (padlock icon)
- Chrome Dev Tools → Console (mixed content warnings)
- [Why No Padlock?](https://www.whynopadlock.com/) (finds mixed content issues)
- Google Search Console → confirm HTTPS property + Security Issues report is clean
