# My Finance Vault — Setup Guide

## What's inside
- **Home Dashboard**: quick-access tiles, total card due, total bank balance, upcoming card dues & bills (7 days), recent transactions
- **Cards**: one-time entity setup (Bank, Card Number, Card Type — auto-detected from number, Expiry, Total Limit). Utilised/Due/Min Due/Due Date are managed automatically via Transactions.
- **Banks**: one-time entity setup (Bank, Account Name, Account Number, Account Type, IFSC with auto branch-fetch, Branch Address/Phone, Starting Balance). Balance updates automatically via Transactions.
- **Transactions**: separate "💰 Add Transaction" button on Cards/Banks screens. Select an existing card/account first, then log Purchase/Payment/Bill Generated (cards) or Credit/Debit (banks). Balance/due updates only on the selected entity.
- **Bills**: Electricity, WiFi/Internet, Rent, Milk, Maintenance, Gas, Mobile Recharge, DTH/OTT, Water, Other — each with a category icon.
- **Govt IDs**: Aadhar, PAN, Driving License, Birth Certificate, Passport, Voter ID, Other — each with a generic icon.
- **Paste SMS**: available inside the Transaction form — paste a bank/card SMS and amount/date auto-fill. The paste box clears itself after use.
- **Security**: 4-digit PIN lock + AES-256 encryption for card numbers, account numbers, and ID numbers.
- **Offline**: all data stays on-device (IndexedDB). Only IFSC lookup needs internet.

## About logos
Official bank/card-network logos are trademarked, so this app uses **stylized, brand-colored badges** (e.g. VISA = navy badge, Mastercard = red-orange badge, bank initials in brand colors) instead of exact logo artwork. If you have your own legally-sourced logo images, they can be swapped in manually.

## Not included yet
- Cheque / card photo scanning (OCR auto-fill) — planned for a future update
- Hindi secondary language toggle — planned for a future update

## APK build steps (PWABuilder)

### Step 1: Host on GitHub Pages (free)
1. Push these files (index.html, manifest.json, sw.js, icon-192.png, icon-512.png) to a public GitHub repo
2. Repo Settings → Pages → Source: "Deploy from a branch" → Branch: main, folder: / (root) → Save
3. Your live URL: `https://<username>.github.io/<repo-name>/`

### Step 2: Package with PWABuilder
1. Go to https://www.pwabuilder.com, paste your GitHub Pages URL, click Start
2. Click "Package for Stores" → Android
3. Keep "New" signing key selected, fill in Key alias/org/country, click Download Package
4. **Save the `signing.keystore` file and its passwords somewhere safe** — needed for every future update

### Step 3: Install & test
- Transfer the `.apk` to your phone and install (allow "Unknown sources" if prompted)
- Test PIN setup, adding a card/bank, adding transactions, and SMS paste

## Updating later without losing data
Keep the **same package name** and **same signing key** every time you rebuild — Android will treat it as an update and your IndexedDB data will remain intact. Always export a backup (Settings → Export Backup) before any major update, just in case.
