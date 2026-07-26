# MisFinanzas+ — Landing

Static landing page for MisFinanzas+ (no build step, no backend).

## Files
- `index.html` — the landing page (self-contained, dark theme).
- `vercel.json` — `cleanUrls` only.
- `favicon.svg` — tab icon.

## Preview locally
Just open `index.html` in a browser.

## Deploy (GitHub + Vercel)

1. **Create the repo & push**
   ```bash
   cd landing
   git init
   git add .
   git commit -m "MisFinanzas+ landing"
   gh repo create misfinanzasplus-landing --public --source=. --push
   # or create the repo on github.com and: git remote add origin <url> && git push -u origin main
   ```

2. **Import to Vercel** → vercel.com/new → pick the repo → **Deploy**
   (Framework preset: **Other**. No build command needed — it's static.)

3. **Add your domain** in Vercel → Project → Settings → Domains → add
   `misfinanzasplus.com`. Vercel shows the DNS records to set at **Namecheap**
   (usually an `A` record for the apex `@` → `76.76.21.21`, and a `CNAME` for
   `www` → `cname.vercel-dns.com`). Follow exactly what Vercel lists.
