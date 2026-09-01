# Version 7 deployment

1. GitHub repository PRSAV/PRS: replace index.html, app.js, styles.css, manifest.webmanifest, sw.js and icon.svg with the v7 files. Commit to main.
2. Keep GitHub Pages on main / root. Site remains https://prsav.github.io/PRS/
3. Cloudflare Worker pv-capture-ai: replace the entire Worker with cloudflare-worker/worker.js and Deploy.
4. Keep existing bindings: DB -> pv-capture-db; Photos -> pv-capture-photos; OPENAI_API_KEY secret.
5. Open the Worker URL. It should report PRS.AssetVerify v7 and version 7.
6. Hard refresh the GitHub Pages app. Version 7 uses fresh v7_* D1 tables, so v6 companies do not appear.
7. On iPhone/Safari allow Camera and Precise Location when prompted.

Default v7 fields:
Sticky: City, Area, Building, Floor Number, Room Number.
Variable: Sub-location, Photo Clicked By, Remarks.
All of these can be edited/deleted from Setting & Master; custom fields can be added.

System roles created per company:
Admin: 24 permissions.
Verifier: 8 field-verification permissions.
Viewer: 4 read/report permissions.
Custom roles may be created from Roles & Permissions.
