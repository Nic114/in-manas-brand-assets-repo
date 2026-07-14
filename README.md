# in-manas brand-assets — hosting

Public, versioned home for logos and product visuals so AI tools can fetch them by stable URL.

## Folder layout
```
brand-assets/
├─ manifest.json          # machine-readable index (name → path + usage)
├─ logo/
│  ├─ logo-full-on-dark.svg      logo-full-on-dark@2x.png
│  ├─ logo-full-on-light.svg     logo-full-on-light@2x.png
│  ├─ logo-mark-on-dark.svg      logo-mark-on-dark@2x.png
│  └─ logo-mark-on-light.svg     logo-mark-on-light@2x.png
└─ screenshots/
   ├─ portal-dashboard.png       portal-dashboard@2x.png
   └─ inno-verse-hub.png         inno-verse-hub@2x.png
```
Add the real files with these exact names (or update `manifest.json` to match).

## Publish (recommended: GitHub + jsDelivr)
1. Create a **public** GitHub repo named `brand-assets` under your org (e.g. `in-manas`).
2. Commit this folder's contents to the `main` branch.
3. Files are instantly live via jsDelivr CDN:
   `https://cdn.jsdelivr.net/gh/<ORG>/brand-assets@main/logo/logo-full-on-dark.svg`
4. Replace `<ORG>` in `manifest.json` `baseUrl` with your GitHub org, commit again.
5. (Optional) For stable releases, tag `v1` and use `@v1` instead of `@main` in the base URL.

**Why jsDelivr:** HTTPS, global CDN, CORS enabled, and `cdn.jsdelivr.net` is on the CSP allowlist that sandboxed AI artifacts enforce — so images load even inside generated HTML/React assets. jsDelivr caches aggressively; after updating a file on `@main`, purge via `https://purge.jsdelivr.net/gh/<ORG>/brand-assets@main/<path>` or bump the version tag.

## Alternatives (no GitHub)
- **Cloudflare Pages / Netlify drop:** drag this folder in, get a URL with CORS + direct file links. Works for web-fetch tools, but NOT inside sandboxed artifacts (not on the CSP allowlist).
- **Branded domain:** point `assets.in-manas.com` at Cloudflare Pages/Netlify or an R2/S3 bucket for a branded URL. Same artifact caveat.

## Requirements checklist (any host)
- [ ] HTTPS, direct file URLs (raw bytes, not a viewer page)
- [ ] CORS: `Access-Control-Allow-Origin: *`
- [ ] Correct content-type (`image/svg+xml`, `image/png`)
- [ ] Stable paths matching `manifest.json`
- [ ] `manifest.json` reachable at `<baseUrl>/manifest.json`
