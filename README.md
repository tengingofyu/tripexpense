# TripExpense

A fast, no-friction travel expense tracker that lives in your browser. Type what you spent in one line — TripExpense handles the currency conversion, categorisation, bill splitting, and reporting.

Built to replace the "WhatsApp yourself the receipt" habit.

**[Open the app →](https://tengingofyu.github.io/tripexpense/)**

---

## Why

Logging expenses on a trip should take two seconds, not two minutes. Most expense apps bury quick entry behind forms, dropdowns, and mandatory fields. TripExpense is one text box:

```
15 lunch visa
```

That's an amount, a description, and a payment card. Done.

## Features

**Quick entry**
- One-line natural input: `15 lunch visa`
- Dual-currency entry: `12000 dinner 18` (foreign amount + home amount)
- Home-currency expenses while overseas: `50 taxi sgd`
- Card shortcuts, auto-categorisation (learns from your history)
- Fill in conversion amounts later — pending entries are flagged

**Trips**
- Personal and work trip types
- Work trips: mark expenses claimable, get a claimables report
- Group trips: split bills evenly or unevenly, see who owes you what, copy a settlement summary straight into your group chat
- Multiple past trips with full history, read-only by default

**Reporting**
- Summary by day, category, and payment card — in both currencies
- Zero-decimal currency handling (JPY, KRW, VND, etc.)
- One-tap formatted Excel export (Summary, Expenses, Settlement/Claimable sheets) via the native share sheet

**Data**
- Local-first: everything works offline, stored on your device
- Optional Google sign-in to sync across devices
- Manual backup/restore (JSON) for moving data anywhere
- Storage-full warnings so data never silently fails to save

## Privacy

- **Default (no sign-in):** all data stays in your browser's local storage. Nothing is uploaded, no account is created, and the developer cannot see anything.
- **Optional sign-in:** trip data syncs to a Google Firebase database so you can use the app across devices. Data is isolated per account — other users cannot see yours. As the project owner, the developer has technical access to the database; if that's not acceptable to you, use the app without signing in.
- No analytics beyond anonymous page views. No ads, no trackers, no data sale. Ever.

## Tech

- Single-file vanilla JavaScript app — no framework, no build step
- `index.html` is the entire application
- [ExcelJS](https://github.com/exceljs/exceljs) (CDN, SRI-pinned) for Excel export
- Firebase Auth + Firestore for optional sync
- Hosted on GitHub Pages

## Run your own

1. Fork or download this repo
2. Serve `index.html` from any static host (GitHub Pages, Netlify, or just open the file)
3. Offline mode works out of the box
4. For sync, create your own [Firebase project](https://console.firebase.google.com), enable Google Auth + Firestore, and replace the `firebaseConfig` block near the top of `index.html` with your own project's config. Set Firestore rules to restrict each user to their own document:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## Status

Personal hobby project, actively used and maintained by one person. Provided as-is, no warranty. Bug reports welcome via Issues.

## License

MIT — see [LICENSE](LICENSE).
