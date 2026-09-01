# PRS.AssetVerify V9 Setup

1. In Cloudflare Worker `pv-capture-ai`, replace the entire Worker code with `cloudflare-worker/worker.js` and Deploy.
2. Keep bindings unchanged: `DB` -> `pv-capture-db`, `Photos` -> `pv-capture-photos`, and existing `OPENAI_API_KEY`.
3. Click Visit. Health must show `service: PRS.AssetVerify v9`, `version: 9`, and all core bindings true. The first V9 request intentionally deletes the pre-V9 companies once, as requested.
4. In GitHub repo `PRSAV/PRS`, replace root frontend files: `index.html`, `app.js`, `styles.css`, `manifest.webmanifest`, `sw.js`, `icon.svg`. Upload `README.md` and `V9_SETUP.md` if desired.
5. Commit, wait for GitHub Pages deployment green check, open https://prsav.github.io/PRS/ and hard-refresh once.
6. From V9 onward do not create new versioned D1 table sets. Future versions should migrate the stable `v8_*` schema in place so company data survives upgrades.

## Backup & Restore
Use hamburger -> Backup & Restore. Download backups before major changes. Restore replaces operational data inside the currently logged-in company but keeps that company's code, username and password. After restore, re-select a member with the restored PIN.

## Existing-company delete
Existing Companies now has Delete. It requires the exact name and PIN of a system Admin for that company.
