# Maintaining getinchly.com

How the Inchly website is built and published. (The public overview is [README.md](README.md).)

The site: the homepage, privacy policy, terms of use and support page. Plain static
HTML with each page's CSS and script inline, no build step, no cookies, analytics or
third-party requests.

| Path | What |
|---|---|
| `index.html` | Homepage |
| `privacy/` | Privacy Policy, including the Consumer Health Data Privacy Policy (`#health`) |
| `terms/` | Terms of Use |
| `support/` | Help and support (the App Store "Support URL") |
| `assets/` | App icon, screenshots, social image, and the Fraunces heading font (SIL Open Font License, see `assets/fraunces-OFL.txt`) |
| `CNAME` | `getinchly.com`, for GitHub Pages |
| `robots.txt`, `sitemap.xml` | For search engines; update `<lastmod>` in the sitemap when a page changes |

The app links to `https://getinchly.com/privacy/`, `/terms/` and the support email `info@snapmeasureai.com` (Inchly is a SnapMeasureAI app, so
all Inchly support and privacy requests go to the parent company's address), and the
store listings use `/privacy/` and `/support/`, so these must be live before the apps are submitted.

## Publish on GitHub Pages

1. Create a repository (for example `getinchly`) and push this folder to its `main` branch.
2. In the repository: **Settings → Pages → Build and deployment**: Source "Deploy from a branch",
   branch `main`, folder `/ (root)`.
3. Under **Custom domain**, enter `getinchly.com` and save (the `CNAME` file already says so).
4. At the domain registrar, add these DNS records:

   | Type | Name | Value |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | AAAA | @ | 2606:50c0:8000::153 |
   | AAAA | @ | 2606:50c0:8001::153 |
   | AAAA | @ | 2606:50c0:8002::153 |
   | AAAA | @ | 2606:50c0:8003::153 |
   | CNAME | www | `<your-github-user-or-org>.github.io` |

5. When the DNS check passes, tick **Enforce HTTPS**. Optionally verify the domain under your
   GitHub account or organization settings (Pages → Verified domains) so no one else can claim it.

## Search engines

After the site is live on https://getinchly.com:

1. Google Search Console: add a **Domain** property for `getinchly.com` (verify with the DNS TXT
   record it gives you), then Sitemaps → submit `https://getinchly.com/sitemap.xml`, and URL
   inspection → `https://getinchly.com/` → Request indexing.
2. Bing Webmaster Tools: "Import from Google Search Console" (this also covers DuckDuckGo and
   Yahoo, which use Bing's index).

SEO notes: the homepage title is 45 characters and the description 136 (Google shows about
50–60 and 150–160 before cutting). Keep "GLP-1" with a plain hyphen in text, not a
non-breaking one, so it matches what people type. The FAQ in the page and the FAQ in the
JSON-LD block in `<head>` must say the same thing; change both together.

## Email

There is no getinchly.com mailbox, and none is needed. Every page, the app and the store
listings use `info@snapmeasureai.com`, so the domain needs no MX records.

## After the apps are live

Paste the two store links into the `STORES` constant at the bottom of `index.html`. Until then
the store buttons read "Coming soon".

## When the app changes

The privacy policy describes exactly what the app stores and sends. If the app starts storing
or sending anything new (a new data type, a new service, analytics), update `privacy/` first
and change the "Last updated" date.
