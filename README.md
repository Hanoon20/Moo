# Moofresh Hanoon — Sales Dashboard

A live, mobile-responsive dashboard for the Moofresh Hanoon goat milk wholesale
business. Connects directly to a Google Sheet via a Google Apps Script Web App
— no backend server, no database, fully free to host.

## Features

- **Overview** — Total Sales, Total Revenue, Pending Payment, Total Bottles,
  Collection Rate gauge, and a "Needs follow-up" list of unpaid/partial buyers
- **Buyers** — searchable buyer list with balance & payment status; tap any
  buyer to see their full purchase history
- **Sales Log** — every sale, newest first, with CSV export
- **New Sale** — create a sale straight from the dashboard (buyer autocomplete,
  today's date filled in automatically, writes directly to the Sales sheet)
- Fully responsive — works on phone, tablet, and desktop from one file

## How it works

- `index.html` is a single self-contained page (no build step, no dependencies)
- It talks to a Google Apps Script Web App deployed from the linked Google
  Sheet, which exposes:
  - `GET` → returns Buyers + Sales as JSON
  - `POST` → creates a new Sale row (used by the "+ New Sale" button)
- The Apps Script also runs automations on the sheet itself: auto-adds new
  buyer names, keeps the Buyer Ledger and Payment Pending table in sync, and
  stamps a Paid Time whenever a sale's status becomes "Paid"

## Setup

1. Open `index.html` in a text editor
2. Find this line near the top of the `<script>` section:
   ```js
   const DEFAULT_API_URL = 'https://script.google.com/macros/s/.../exec';
   ```
3. Replace it with your own Apps Script Web App URL if you fork this for a
   different sheet (already set for Moofresh Hanoon)
4. Deploy — this repo is connected to Netlify, so pushing to `main` triggers
   an automatic redeploy

## Updating

Whenever the dashboard changes:

```bash
git add index.html
git commit -m "Update dashboard"
git push
```

Netlify picks up the push automatically — no manual redeploy needed.
