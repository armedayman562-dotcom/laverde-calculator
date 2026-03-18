# La Verde Calculator — Deployment Guide
## Files in this folder
- `index.html`      → The calculator app
- `vercel.json`     → Vercel configuration
- `prices-template.csv` → Upload this to Google Sheets

---

## STEP 1 — Google Sheets (prices database)

1. Go to sheets.google.com → New spreadsheet
2. Name it: "La Verde Prices"
3. Import prices-template.csv:
   File → Import → Upload → prices-template.csv
   → "Replace spreadsheet" → Import

4. Edit the PPM column (column C) whenever prices change.
   - ppm = Price per square meter in EGP
   - amin/amax = area range in m²
   - adef = default area shown on slider

5. Publish to web:
   File → Share → Publish to web
   → Sheet1 → CSV → Publish
   → COPY the URL (looks like: https://docs.google.com/...export?format=csv...)

6. Open index.html, find this line (~line 1730):
      const SHEET_CSV_URL = '';
   Replace the empty string with your URL:
      const SHEET_CSV_URL = 'https://docs.google.com/...your-url...';

7. Save index.html

---

## STEP 2 — Change the Password

Open index.html, find this line (~line 1720):
    const SALES_PASS = 'laverde2025';
Change 'laverde2025' to whatever password you want.
Save index.html.

---

## STEP 3 — Deploy on Vercel

1. Go to vercel.com → Log in → Add New Project
2. Choose "Deploy without Git" (drag & drop option)
   OR connect a GitHub repo containing these files

3. Drag this entire folder onto the Vercel upload area
4. Click Deploy
5. Vercel gives you a URL like: laverde-calc.vercel.app ✓

---

## STEP 4 — Connect Namecheap Domain

In Vercel:
1. Project → Settings → Domains
2. Add your domain (e.g. calc.laverde-eg.com)
3. Vercel shows you a CNAME value to add

In Namecheap:
1. Domain List → Manage → Advanced DNS
2. Add Record:
   Type:  CNAME
   Host:  calc   (or @ for root domain)
   Value: cname.vercel-dns.com
3. Save — DNS propagates in 5-30 minutes

---

## HOW TO UPDATE PRICES LATER

Just edit the Google Sheet → Save.
The calculator fetches fresh prices every time it loads.
No need to redeploy anything.

---

## HOW TO CHANGE PASSWORD LATER

Edit index.html → Change SALES_PASS → Re-upload to Vercel.
Vercel auto-deploys on new upload. Takes 30 seconds.
