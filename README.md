# My Finance Vault — Setup Guide

## What's inside
- **Home Dashboard**: total card due, total bank balance, Cards overview, and Pending Bills (all unpaid bills, sorted by due date).
- **Cards**: one-time entity setup (Bank, Card Number, Card Type — auto-detected from number, Expiry, Total Limit). Utilised/Due/Min Due/Due Date are managed automatically — Due/Min Due/Due Date come from a "Credit Card Bill" entry in the Bills tab; Utilised/Due also move with Purchase/Payment transactions.
- **Banks**: one-time entity setup (Bank, Account Name, Account Number, Account Type, IFSC with auto branch-fetch, Branch Address/Phone, Starting Balance). Balance updates automatically via Transactions.
- **Transactions**: "💰 Add Transaction" button on Cards/Banks screens. Select an existing card/account first, then log Purchase/Payment (cards) or Credit/Debit (banks). Each transaction can be **edited or deleted later** — open the Card/Account (tap it in the list) to see its full Transaction History with Edit/Delete buttons; editing or deleting automatically re-adjusts the balance/due correctly.
- **Bills**: Electricity, WiFi/Internet, Rent, Milk, Maintenance, Gas, Mobile Recharge, DTH/OTT, Water, Other, and **Credit Card Bill** (linked to a specific card — this is now the ONLY place a card's statement/due is generated, so there's no more duplicate entry between Transactions and Bills).
- **Govt IDs**: Aadhar, PAN, Driving License, Birth Certificate, Passport, Voter ID, Other.
- **Paste SMS**: available in the Transaction form and the Bill form — paste a bank/card SMS and amount/date (and min-due for Credit Card Bill) auto-fill. The paste box clears itself after use.
- **Security**: 4-digit PIN lock + AES-256 encryption for card numbers, account numbers, and ID numbers.
- **Offline**: all data stays on-device (IndexedDB). Only IFSC lookup needs internet.
- **Back button**: closes any open form first, then returns to Home, then asks for confirmation before exiting the app.

## Adding your own logos (optional)
This app can display real logo images instead of the built-in colored badges — you add the image files yourself (Anthropic policy doesn't allow generating or embedding official trademarked logos on your behalf, but the app is built to use your own files automatically once present).

Create these folders in the same place as `index.html` in your GitHub repo, and add PNG files named exactly like this (all lowercase, spaces/slashes replaced with a single dash):

**`bank-logo/`** — filename = bank name, e.g.:
`sbi.png`, `hdfc-bank.png`, `icici-bank.png`, `axis-bank.png`, `kotak-mahindra.png`, `punjab-national-bank.png`, `bank-of-baroda.png`, `canara-bank.png`, `union-bank-of-india.png`, `idfc-first-bank.png`, `yes-bank.png`, `indusind-bank.png`, `rbl-bank.png`, `federal-bank.png`, `idbi-bank.png`, `bank-of-india.png`, `indian-bank.png`, `central-bank-of-india.png`, `au-small-finance-bank.png`, `roar-bank.png`

**`id-logo/`** — filename = ID type, e.g.:
`aadhar.png`, `pan.png`, `driving-license.png`, `birth-certificate.png`, `passport.png`, `voter-id.png`

**`bill-logo/`** — filename = the Bill's **Nickname** if you set one (e.g. nickname "Airtel Wifi" → `airtel-wifi.png`), otherwise the Biller Type (e.g. `electricity.png`, `mobile-recharge.png`, `credit-card-bill.png`).

If a matching file isn't found, the app automatically falls back to the built-in colored emoji badge — nothing breaks either way.

## APK build steps (PWABuilder)

### Step 1: Host on GitHub Pages (free)
1. Push these files (index.html, manifest.json, sw.js, icon-192.png, icon-512.png, and optionally your `bank-logo/`, `id-logo/`, `bill-logo/` folders) to your public GitHub repo — **make sure index.html's "last updated" timestamp changes after upload**, otherwise the upload didn't actually replace it.
2. Repo Settings → Pages → Source: "Deploy from a branch" → Branch: main, folder: / (root) → Save
3. Your live URL: `https://<username>.github.io/<repo-name>/`

### Step 2: Package with PWABuilder
1. Go to https://www.pwabuilder.com, paste your GitHub Pages URL, click Start
2. Click "Package for Stores" → Android
3. Under Signing key, choose **"Use mine"** (not "New") and upload your saved `signing.keystore` + its passwords — this keeps every update installable over the previous version without losing data
4. Click Download Package

### Step 3: Install & test
- Transfer the `.apk` to your phone and install directly over the old one (don't uninstall first) — your data stays intact
- Test PIN, adding a card/bank, adding a Credit Card Bill, transactions, edit/delete transaction, and the back button behavior

## Updating later without losing data
Keep the **same package name** and **same signing key** every time you rebuild. Always export a backup (Settings → Export Backup) before any major update, just in case.
