# The Learning LeadAbility — website

Static site for thelearningleadability.org, hosted on Cloudflare Pages.

- `public/` — everything that gets deployed
- `public/_redirects` — controls where the QR code goes
- `qr/` — the QR code (points to https://thelearningleadability.org/about)

## Run locally

`_redirects` is applied by the server, so it won't work if you open
`index.html` directly. Run the Cloudflare dev server instead:

    npm install
    npm run dev

Then open http://localhost:8788 (and http://localhost:8788/about for the PDF).

## Updating the PDF (QR code never changes)

1. Put the new PDF in `public/files/`, e.g. `tll-company-profile-2027.pdf`
2. Edit `public/_redirects` so `/about` points to the new file
3. Commit and push — Cloudflare redeploys automatically

Keep the redirect as `302`. A `301` gets cached by phones and they'd keep opening the old PDF.

## First-time deploy

1. Push this repo to GitHub.
2. Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git → pick the repo.
   Build command: none. Build output directory: `public`.
3. Add the domain to Cloudflare: dashboard → Add a domain → `thelearningleadability.org`
   (Free plan). Cloudflare imports the existing DNS records — check the MX/TXT
   (email) records came across.
4. At Squarespace → Domains → thelearningleadability.org → DNS → Nameservers →
   use custom nameservers, and enter the two Cloudflare gives you. Takes up to a few hours.
5. Once the domain is active in Cloudflare: Pages project → Custom domains → add
   `thelearningleadability.org` and `www.thelearningleadability.org`.

Test: scan `qr/about-qr.png` with a phone — it should open the PDF.
