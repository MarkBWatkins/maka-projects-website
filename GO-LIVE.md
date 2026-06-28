# 🚀 Go-Live Checklist — makaprojects.co.nz

Plain-English steps to put the site online. Follow them top to bottom.
Nothing here touches your email — your Microsoft 365 inbox keeps working throughout.

You'll do three things:
1. Get the site onto Netlify (so it has a temporary live address).
2. Tell Netlify your real domain is `makaprojects.co.nz`.
3. Add two DNS records at 1st Domains so the domain points at Netlify.

⏱️ Budget ~20 minutes, plus up to a few hours for DNS to spread worldwide.

---

## STEP 1 — Get a Netlify account (free)

1. Go to **https://app.netlify.com/signup**
2. Sign up. The easiest option is **"Sign up with GitHub"** (recommended — it makes
   the auto-update setup in Step 2 one-click). Email/password also works.
3. Verify your email if asked.

---

## STEP 2 — Put the site on Netlify

You have **two ways**. Option A gives you automatic updates forever (recommended).
Option B is a 60-second shortcut if you want it live *right now* and will wire up
auto-updates later.

### ✅ Option A — Connect the code repo (auto-updates on every change) — RECOMMENDED

This needs the project pushed to GitHub first. **It is not pushed yet** (this computer
doesn't have GitHub set up). One-time setup:

1. Create a free GitHub account at **https://github.com/signup** (skip if you have one).
2. On GitHub, click **+ → New repository**. Name it `maka-website` (or anything).
   Set it to **Private**. **Do NOT** tick "add a README" — the repo already has one.
   Click **Create repository**.
3. GitHub shows a "…push an existing repository" box. Copy the two lines it gives you.
   They look like this (your username instead of `YOURNAME`):
   ```
   git remote add origin https://github.com/YOURNAME/maka-website.git
   git push -u origin main
   ```
   Run them in this project folder (`C:\Maka Projects\website`). It'll ask you to log in
   to GitHub the first time — follow the browser prompt.
   > The repo is already committed and ready — you're only adding the remote and pushing.
4. Back in Netlify: **Add new site → Import an existing project → Deploy with GitHub**,
   authorise it, and pick your `maka-website` repo.
5. Netlify reads `netlify.toml` automatically. Leave build command **blank** and
   publish directory **`.`** (already set for you). Click **Deploy**.
6. Done. **From now on, any change you commit and push goes live automatically** —
   no uploading, no clicking.

### ⚡ Option B — Drag-and-drop (live in 60 seconds, no GitHub)

Use this to go live immediately; you can switch to Option A anytime.

1. In Netlify: **Add new site → Deploy manually**.
2. Open the folder `C:\Maka Projects\website` in File Explorer.
3. Drag the **whole folder** onto the Netlify drop zone in the browser.
4. It deploys instantly and gives you a temporary address like
   `https://random-name-12345.netlify.app`. Check the site looks right.
   > Downside: to update the site later you have to drag the folder again each time.
   > Option A avoids that — that's why it's recommended.

➡️ **Either way, note your temporary Netlify address** (e.g.
`something-12345.netlify.app`) — you need it for the DNS step. You can rename it under
**Site configuration → Change site name** to something tidy like
`maka-projects.netlify.app`.

---

## STEP 3 — Tell Netlify your domain

1. In your Netlify site: **Domain management → Add a domain**.
2. Enter **`makaprojects.co.nz`** and add it.
3. When Netlify asks how to manage DNS, choose **"Add a domain you already own"** and,
   if offered, **set up your DNS records manually / use external DNS**.
   ⚠️ **Do NOT choose "Use Netlify DNS" / nameservers.** That would move ALL your DNS
   to Netlify, including email — we don't want that.
4. Netlify will then show records to add (an A record and a CNAME). They should match
   Step 4 below. If Netlify shows a *different* IP than `75.2.60.5`, use the one
   **Netlify shows you** — it knows your specific setup.

---

## STEP 4 — Add the DNS records at 1st Domains

Log in at **https://1stdomains.nz** → your domain `makaprojects.co.nz` → **DNS / Zone
management** (sometimes called "Advanced DNS" or "Manage DNS").

Add these **two** records:

| # | Type  | Host / Name | Value / Points to                         | TTL          |
|---|-------|-------------|-------------------------------------------|--------------|
| 1 | **A** | `@` (blank) | `75.2.60.5`                               | default/3600 |
| 2 | **CNAME** | `www`   | `your-site-name.netlify.app`  *(your Netlify address from Step 2)* | default/3600 |

Notes:
- Record 1 (`@`) is the bare domain `makaprojects.co.nz`. Some panels want the host left
  blank instead of `@` — both mean the same thing.
- Record 2 (`www`) is `www.makaprojects.co.nz`. Its value is **your** Netlify subdomain
  (the `xxxx.netlify.app` address), **not** a literal — paste your real one.
- **If 1st Domains offers an `ALIAS` or `ANAME` record type**, you can instead point
  `@` to `apex-loadbalancer.netlify.com` (slightly better than the raw IP). If there's
  no ALIAS/ANAME option, the A record to `75.2.60.5` above is correct and fine.

### ⛔ DO NOT TOUCH — your email records

Leave every **MX** record exactly as-is. Also leave any **TXT** records that mention
`spf`, `DKIM`, or `microsoft`, and any `autodiscover` / `lyncdiscover` / `enterpriseregistration`
CNAMEs. **These run your Microsoft 365 email.** You are only *adding* the two website
records above — you are not editing or deleting anything else.

> Quick sanity check: before you save, your MX record(s) should still point at something
> like `makaprojects-co-nz.mail.protection.outlook.com`. If they do, your email is safe.

---

## STEP 5 — Set www → apex redirect & turn on HTTPS

Back in Netlify, after DNS is added:

1. **Domain management** → set **`makaprojects.co.nz` as the Primary domain**.
   Netlify will automatically redirect `www.makaprojects.co.nz` → `makaprojects.co.nz`
   (so both addresses work and land in the same place). Nothing else to configure.
2. Netlify auto-provisions a free **HTTPS (SSL) certificate** once it sees the DNS.
   This can take a few minutes up to an hour. Wait until it says **"Certificate: Active"**.
   Then tick **"Force HTTPS"** so visitors always get the secure version.

---

## STEP 6 — Verify it's live

- DNS changes can take **anywhere from a few minutes to a few hours** (occasionally up
  to 24h) to spread. Be patient if it's not instant.
- Visit **https://makaprojects.co.nz** and **https://www.makaprojects.co.nz** —
  both should load the site, with a padlock in the address bar.
- **Send yourself a test email** to `markw@makaprojects.co.nz` and reply from it, to
  confirm email is unaffected (it will be — you never touched the MX records).

---

## Updating the site later

- **If you used Option A (GitHub):** edit the files, then in this folder run
  `git add -A`, `git commit -m "your note"`, `git push`. Live in about a minute. Done.
- **If you used Option B (drag-drop):** drag the folder onto Netlify again, or switch to
  Option A whenever you're ready for hands-off updates.

---

## Quick reference

| Thing | Value |
|---|---|
| Primary domain | `makaprojects.co.nz` |
| Apex A record | `75.2.60.5` |
| www CNAME target | `your-site-name.netlify.app` |
| Email | Microsoft 365 — **MX untouched** |
| Host | Netlify |
| Site files | this folder (`index.html` is the page) |
