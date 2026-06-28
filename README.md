# Maka Projects — Website

The public marketing site for **Maka Projects** — civil infrastructure project direction,
NZS 3910 commercial management and delivery leadership across the central North Island
(Waikato & Bay of Plenty), New Zealand.

**Live site:** https://makaprojects.co.nz
**Director / contact:** Mark Watkins — markw@makaprojects.co.nz

---

## What this is

A single-page, hand-written static site. No framework, no build step — just one
`index.html` with inline CSS, plus a handful of static assets.

```
index.html      The whole site (HTML + inline CSS)
favicon.svg     Vector favicon (modern browsers)
favicon.ico     Fallback favicon (legacy / bookmarks)
og-image.png    1200×630 social-share preview image
robots.txt      Search-engine crawl rules
sitemap.xml     Sitemap for search engines
netlify.toml    Netlify hosting config (publish dir + headers)
```

## Hosting & deployment

Hosted on **Netlify** with **Git-backed continuous deployment**.

Once connected, **every push to the `main` branch deploys automatically** — there is
nothing to build or upload by hand. To update the site: edit the files, commit, push.

```bash
git add -A
git commit -m "Update copy"
git push          # Netlify builds & publishes within ~1 minute
```

## Editing the site

- **Copy / text & layout:** all in `index.html`.
- **Brand colours:** the `:root` CSS variables at the top of `index.html`
  (accent orange `#e8731a`, ink `#1a1d21`).
- **Social preview image:** replace `og-image.png` (keep it 1200×630).
- **Contact email:** `markw@makaprojects.co.nz` (in the contact section and the
  structured-data block in `<head>`).

## Local preview

It's a static file — just open `index.html` in a browser. Or serve it:

```bash
python -m http.server 8080
# then visit http://localhost:8080
```

## Domains & email

- Primary public domain: **makaprojects.co.nz** (also owns `makaprojects.nz`,
  `makaproperty.co.nz`, `makaproperty.nz`).
- DNS is managed at **1st Domains**.
- **Email runs on Microsoft 365 — the MX records must NOT be changed.** Only the
  website A/CNAME records point at Netlify. See `GO-LIVE.md`.

## First-time go-live

See **[GO-LIVE.md](GO-LIVE.md)** for the exact, plain-English steps to put the site
online (Netlify signup, connecting this repo, and the DNS records to add at 1st Domains).
