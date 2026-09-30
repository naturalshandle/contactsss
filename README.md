# A. Sunada – Contact Card

A static contact page: scan the QR code → open the page → tap **Add to Contacts** → the phone imports `sunada.vcf`.

No backend, no build step, no framework.

## Files

| File          | Purpose                                                          |
|---------------|------------------------------------------------------------------|
| `index.html`  | Contact page (name, title, phone, button, QR code)               |
| `sunada.vcf`  | vCard 3.0 contact file                                           |
| `vercel.json` | Serves `.vcf` files as `text/vcard` so phones open them as contacts |

The QR code is generated in the browser (via [qrcodejs](https://github.com/davidshimjs/qrcodejs) from cdnjs) and always encodes the URL the page is currently served from. Once deployed, it automatically points to your Vercel URL.

## Run locally

Any static file server works. Pick one:

```bash
# Node.js
npx serve .

# Python 3
python -m http.server 8000
```

Then open the printed URL (e.g. http://localhost:3000 or http://localhost:8000).

Note: locally the QR code encodes `localhost`, so it won't work when scanned from a phone. To test on a phone, open `http://<your-computer-LAN-IP>:8000` from the phone on the same Wi-Fi — or just deploy.

## Deploy to Vercel

### Option A – Vercel CLI

```bash
npm i -g vercel
vercel login
vercel          # preview deploy; accept defaults (no build command, output dir ".")
vercel --prod   # production deploy
```

### Option B – GitHub + Vercel dashboard

1. Push this folder to a GitHub repository.
2. Go to https://vercel.com/new and import the repository.
3. Framework Preset: **Other**. Leave Build Command and Output Directory empty.
4. Click **Deploy**.

## After deploying

1. Open your production URL (e.g. `https://your-project.vercel.app`).
2. The QR code on the page now points to that URL — print or share it.
3. Scan it with a phone, tap **Add to Contacts**:
   - **iPhone (Safari):** opens the contact preview → tap *Create New Contact*.
   - **Android (Chrome):** downloads `sunada.vcf` → tap the download to open it in Contacts.
