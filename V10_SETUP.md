# PRS.AssetVerify V10 Setup

1. In Cloudflare Worker `pv-capture-ai`, replace the entire Worker code with `cloudflare-worker/worker.js` and Deploy.
2. Keep bindings unchanged: `DB` -> `pv-capture-db`, `Photos` -> `pv-capture-photos`, and existing `OPENAI_API_KEY`.
3. Click Visit. Health must show `service: PRS.AssetVerify v10`, `version: 10`, and core bindings true.
4. V10 does not reset existing company data. It migrates the stable `v8_*` schema in place and preserves V9 data.
5. In GitHub repo `PRSAV/PRS`, replace root frontend files: `index.html`, `app.js`, `styles.css`, `manifest.webmanifest`, `sw.js`, `icon.svg`.
6. Commit, wait for GitHub Pages deployment, open https://prsav.github.io/PRS/ and hard-refresh once.

## V10 role rules
- At least one active system Admin is compulsory at all times.
- The last active Admin cannot be reassigned or deleted.
- System-generated Admin, Verifier and Viewer roles can be edited, but their internal identities remain stable.
- The Admin role retains core role/member-management permissions required to avoid locking the company out.
- Role assignment validates the complete resulting member-role map before applying updates.

## Network reliability
The V10 frontend converts raw browser `Failed to fetch` failures into clear connectivity messages and avoids protected calls before member selection. A real internet, DNS, browser, or Cloudflare outage can still prevent requests from reaching the Worker.

## Backup & Restore
Backup & Restore remains available. Restore validates data before replacement and preserves the current company code, username and password.
