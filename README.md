# MisFinanzas+ — Landing

Static landing page for MisFinanzas+ (no build step). Also proxies the iOS
Shortcut ingest endpoint at `/pago`.

## Files
- `index.html` — the landing page (self-contained, dark theme).
- `vercel.json` — `cleanUrls` + the `/pago` → Supabase Edge Function rewrite.
- `favicon.svg` — tab icon.

## Preview locally
Just open `index.html` in a browser. (The `/pago` rewrite only works once
deployed to Vercel — it's a server-side proxy.)

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

4. **Verify the endpoint** once deployed:
   ```bash
   curl -s -X POST "https://misfinanzasplus.com/pago" \
     -H "Authorization: Bearer <YOUR_SHORTCUT_TOKEN>" \
     -H "Content-Type: application/json" \
     -d '{"amount": 4990, "merchant": "Prueba proxy", "idempotency_key": "proxy-001"}'
   # expect: {"ok":true,"id":"..."}
   ```
   Then point your iOS Shortcut at `https://misfinanzasplus.com/pago`.

## Notes
- The `/pago` rewrite forwards the POST (method, body, `Authorization`) straight
  to the Supabase Edge Function `ingest-manual` — no secrets live in this repo.
- To change the endpoint path (e.g. `/api/pago`), edit `source` in `vercel.json`.
