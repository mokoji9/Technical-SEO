# Fix Guide: Cloudflare (or Similar) Bot Protection Blocking Search Crawlers

**Category:** Crawlability

## 1. What's wrong

Your site is protected by Cloudflare (or a similar security/CDN service) with bot-protection
features like "Bot Fight Mode," "Super Bot Fight Mode," or a custom firewall rule turned on.
These are designed to block scrapers and malicious bots — but if configured too aggressively,
they can also challenge or outright block **legitimate search engine crawlers** like Googlebot
and Bingbot, along with SEO audit tools.

## 2. Why it matters

This is one of the most damaging technical SEO problems there is, because it's invisible from
a normal browser: you and your visitors see the site working fine, while search engines are
silently being blocked or served an interactive "prove you're human" challenge page instead of
your real content. Googlebot **cannot solve CAPTCHAs or interactive challenges** — if it hits
one, it gives up, and your pages stop getting crawled and can eventually drop out of the index
entirely.

## 3. How to check it yourself

1. **Check Google Search Console → Settings → Crawl Stats.** Look for a spike in "blocked"
   or failed crawl requests, or a host availability problem.
2. **Check Google Search Console → Page Indexing report** for pages excluded with errors like
   "Blocked due to unauthorized request (401)" or a sudden drop in indexed pages.
3. **Test with curl using different user-agents** (from a terminal):
   ```bash
   curl -A "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)" -o /dev/null -w "%{http_code}\n" https://yourdomain.com/
   curl -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/120.0.0.0" -o /dev/null -w "%{http_code}\n" https://yourdomain.com/
   ```
   If the Googlebot user-agent returns a 403/503 or something very different from the browser
   user-agent, that's a strong signal (though not 100% proof — see note below).
4. **Use Google Search Console's URL Inspection tool → "Test Live URL"** — this uses Google's
   real infrastructure and is the most reliable check. If it fails to fetch or renders a
   challenge page, that's confirmed.

> **Note:** A user-agent spoofed with `curl` doesn't come from Google's real IP ranges, so a
> well-configured bot-protection service *should* still block a fake Googlebot — that's
> correct, expected behavior, not a bug. The `curl` test is a useful early signal, but Google
> Search Console's "Test Live URL" (using Google's real crawler) is the only fully reliable
> way to confirm whether the *real* Googlebot is affected.

## 4. Step-by-step fix (Cloudflare)

1. Log into the [Cloudflare dashboard](https://dash.cloudflare.com/) for the domain.
2. Go to **Security → Bots**.
3. Confirm **"Verified Bots"** is allowed through (this is what lets real Googlebot/Bingbot
   bypass challenges — Cloudflare verifies them via reverse-DNS against Google's/Microsoft's
   published IP ranges).
4. If **Bot Fight Mode** or **Super Bot Fight Mode** is on, check its configured action for
   "Definitely Automated" / "Likely Automated" traffic — make sure it isn't set to block
   verified search bots.
5. Go to **Security → WAF → Custom Rules** and check for any custom rule that might be
   blocking based on IP range, ASN, or missing headers/cookies that a crawler wouldn't send
   (e.g. a rule requiring a specific cookie or JS challenge on every request).
6. If using **"I'm Under Attack Mode"**, turn it off unless actively needed — it JS-challenges
   every visitor, including crawlers, with no exceptions.
7. Under **Security → Bots → Verified Bots**, you can also explicitly allowlist by user-agent
   + IP range as a belt-and-suspenders approach, though the Verified Bots toggle should handle
   this automatically for major search engines.
8. Save changes.

## 5. How to verify the fix worked

1. Re-run the `curl` user-agent test from Step 3 — a Googlebot UA request behind a legitimate
   Google IP would now pass, though you can't fully simulate that with curl.
2. In Google Search Console, use **URL Inspection → Test Live URL** on a few key pages —
   confirm it fetches successfully and renders the real page (not a challenge screen).
3. Watch **Search Console → Crawl Stats** over the next few days for crawl requests returning
   to normal (no unusual spike in errors or "blocked" responses).
4. Re-run an automated crawl/audit tool against the site — it should now return real content
   instead of a 403.

## 6. Tools to double-check

- Google Search Console → URL Inspection ("Test Live URL") and Crawl Stats report
- Cloudflare dashboard → Security → Bots / WAF Custom Rules
- `curl` with different user-agents (early signal only, not conclusive on its own)
