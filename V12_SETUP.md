# PRS.AssetVerify V12 deployment

## 1. Cloudflare Worker
Open Cloudflare > Workers & Pages > `pv-capture-ai` > Edit code. Replace the Worker with `cloudflare-worker/worker.js`, then Deploy.

Keep existing bindings unchanged:
- `DB` -> existing D1 database (`pv-capture-db`)
- `Photos` -> existing R2 bucket (`pv-capture-photos`)
- `OPENAI_API_KEY` -> existing secret

The health URL must show `service: PRS.AssetVerify v12` and `version: 12`.

**Data safety:** V12 has no startup company wipe/reset. It continues to use the existing `v8_*` tables and existing R2 keys. Company deletion only occurs if a user explicitly runs a Delete Company action.

## 2. GitHub Pages frontend
Replace these files in the PRS repository root:
- `index.html`
- `app.js`
- `styles.css`
- `sw.js`
- `manifest.webmanifest`
- `icon.svg`

Commit the changes. Then open `https://prsav.github.io/PRS/` and press Ctrl+Shift+R once.

## 3. V12 verification flow
Take Photo / Gallery / Scan -> Sticky Fields -> Variable Fields appear automatically -> asset details -> Save Verification -> Export Excel.

GPS begins automatically. Latitude, Longitude and GPS Accuracy are optional and may remain blank.
