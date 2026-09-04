# Checklist: Security & Internationalization

## Security
- [ ] Site is served entirely over HTTPS
- [ ] HTTP automatically redirects to HTTPS (301, not 302)
- [ ] SSL certificate is valid and not expiring soon
- [ ] No mixed content warnings (HTTP resources on HTTPS pages)
- [ ] No security warnings in Google Search Console

## Status codes
- [ ] All important pages return 200
- [ ] Removed pages return 410 (or 404) rather than redirecting everything to the homepage
- [ ] Redirects use 301 (permanent) not 302 (temporary) unless truly temporary
- [ ] No redirect loops

## Internationalization (if applicable)
- [ ] `hreflang` tags are implemented correctly for all language/region variants
- [ ] hreflang tags are reciprocal (each page references the others, and itself)
- [ ] `x-default` is set where appropriate
- [ ] Language/region targeting matches actual page content

**Related fix guides:** `fixes/security-international/`
