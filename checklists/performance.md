# Checklist: Performance / Core Web Vitals

- [ ] Largest Contentful Paint (LCP) is under 2.5s
- [ ] Interaction to Next Paint (INP) is under 200ms
- [ ] Cumulative Layout Shift (CLS) is under 0.1
- [ ] Time to First Byte (TTFB) is fast (under ~0.8s)
- [ ] Images are compressed and served in modern formats (WebP/AVIF)
- [ ] Images use `width`/`height` attributes to prevent layout shift
- [ ] Lazy loading is used for below-the-fold images
- [ ] Render-blocking CSS/JS is minimized or deferred
- [ ] A CDN is used for static assets
- [ ] Browser caching headers are set correctly
- [ ] Unused CSS/JS is minimized (code splitting)
- [ ] Fonts are optimized (preload, font-display: swap)
- [ ] Server/hosting isn't the bottleneck (check TTFB under load)

**Related fix guides:** `fixes/performance/`
