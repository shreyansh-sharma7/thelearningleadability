# The Learning LeadAbility — website

Static site for thelearningleadability.org, hosted on Netlify.

- `public/` — everything that gets deployed
- `public/_redirects` — controls where the QR code goes
- `qr/` — the QR code (points to https://thelearningleadability.org/about)

## Updating the PDF (QR code never changes)

1. Export the new PDF and put it in `public/files/`, e.g. `tll-company-profile-2027.pdf`
2. Edit `public/_redirects` so `/about` points to the new file
3. Commit and push — Netlify redeploys in ~30 seconds

Keep the redirect as `302`. A `301` gets cached by phones and they'd keep opening the old PDF.

## First-time deploy

1. Push this repo to GitHub.
2. Netlify → Add new site → Import from GitHub → pick the repo. The publish folder
   (`public`) is already set in `netlify.toml`, no build command needed.
3. Netlify → Domain management → Add domain `thelearningleadability.org`.

## DNS at Squarespace

Squarespace → Domains → thelearningleadability.org → DNS → Custom records.
Remove any existing Squarespace default A/CNAME records for `@` and `www` first
(leave MX/TXT records alone — those are email).

| Host | Type  | Value                          |
|------|-------|--------------------------------|
| @    | A     | 75.2.60.5                      |
| www  | CNAME | <your-site-name>.netlify.app   |

Then in Netlify, wait for the domain to verify and click "Provision certificate"
if HTTPS isn't enabled automatically. DNS can take up to a few hours.

Test: scan `qr/about-qr.png` with a phone — it should open the PDF.
