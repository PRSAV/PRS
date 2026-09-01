# IMPORTANT – Guided Capture Flow Fix

If your Cloudflare Worker already reports PRS.AssetVerify v11, DO NOT replace the Worker for this flow fix. Upload the frontend files (index.html, app.js, styles.css, sw.js, manifest.webmanifest, icon.svg) to GitHub. Existing companies remain in D1/R2 and are not deleted by this frontend update.

# PRS.AssetVerify V11 Setup

## 1. Cloudflare Worker

Replace the Worker code with `cloudflare-worker/worker.js`. Keep these bindings unchanged:

- `DB` → `pv-capture-db`
- `Photos` → `pv-capture-photos`
- `OPENAI_API_KEY` → existing Secret

Deploy and open the Worker URL. Health must show `service: PRS.AssetVerify v11` and `version: 11`.

**Data safety:** V11 has no startup company-deletion routine. Existing companies are preserved.

## 2. GitHub Pages frontend

Upload/replace the root files:

- `index.html`
- `app.js`
- `styles.css`
- `manifest.webmanifest`
- `sw.js`
- `icon.svg`

Do not upload the `cloudflare-worker` folder to the Pages root.

After GitHub Pages deploys, hard-refresh (`Ctrl+Shift+R`). If an older UI remains, unregister the old service worker / clear site data once.

## 3. V11 checks

- Open an existing company and confirm it still exists.
- Try changing the only Admin to Verifier: it must be blocked.
- Add/promote a second Admin, then changing the first Admin should be allowed.
- Edit Admin/Verifier/Viewer from Roles & Permissions.
- Reassign a member through a role and confirm no raw `Failed to fetch` message appears for a normal validation error.
- Capture/upload a photo: the review should open immediately with `Continue to Variable Details →`.
- Continue, fill variable fields, review asset rows, and save the verification.
