# The Learning LeadAbility — website

Static site for thelearningleadability.org, hosted on Cloudflare Workers (static assets).

- `public/` — everything that gets deployed
- `public/_redirects` — controls where the QR code goes
- `qr/` — the QR code (points to https://thelearningleadability.org/about)

## Run locally

`_redirects` is applied by the server, so it won't work if you open
`index.html` directly. Run the Cloudflare dev server instead:

    npm install
    npm run dev

Then open http://localhost:8787 (and http://localhost:8787/about for the PDF).

## Updating the PDF (QR code never changes)

1. Put the new PDF in `public/files/`, e.g. `tll-company-profile-2027.pdf`
2. Edit `public/_redirects` so `/about` points to the new file
3. Commit and push — Cloudflare redeploys automatically

Keep the redirect as `302`. A `301` gets cached by phones and they'd keep opening the old PDF.

## First-time deploy

1. Push this repo to GitHub.
2. Cloudflare dashboard → Workers & Pages → Create → Import a repository → pick the repo.
   Deploy command: `npx wrangler deploy` (the default). `wrangler.toml` points it at `public/`.
   The project name in Cloudflare must match `name` in `wrangler.toml`.
3. Domain is on Cloudflare DNS (nameservers changed at Squarespace → Domains → DNS → Nameservers).
   Keep the Google MX/SPF/DKIM records; remove any old Squarespace A/CNAME records.
4. Worker → Settings → Domains & Routes → Add → Custom domain:
   `thelearningleadability.org` and `www.thelearningleadability.org`.

Test: scan `qr/about-qr.png` with a phone — it should open the PDF.
