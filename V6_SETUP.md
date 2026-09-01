# PRS.AssetVerify v6 setup

Frontend target: https://prsav.github.io/PRS/
Worker: https://pv-capture-ai.mahipal-office21.workers.dev

## GitHub
1. Sign in to the GitHub account/organization `prsav`.
2. Create a public repository named `PRS`.
3. Upload `index.html`, `app.js`, `styles.css`, `manifest.webmanifest`, `sw.js`, and `icon.svg` to the repository root.
4. Repository Settings > Pages > Deploy from branch > `main` > `/ (root)`.
5. The site should become `https://prsav.github.io/PRS/`.

## Cloudflare
Keep existing bindings:
- `DB` -> `pv-capture-db`
- `Photos` -> `pv-capture-photos`
- Secret `OPENAI_API_KEY`

Replace the complete Worker code with `cloudflare-worker/worker.js` and Deploy.
The Worker health response should say `PRS.AssetVerify v6` and `frontendOrigin: https://prsav.github.io`.

## v6 authentication model
- Each company has one company username and company password.
- Team members have only Name + Role (Admin / Verifier).
- After company login, the app asks which team member is using the app.
- Admin/Verifier rights are applied based on that selected team member.
- Forgot Company Password is visible on the company-login modal.

Important: because the company credential is shared, anyone who knows it can technically select any listed team member. If strict identity security is required later, add a per-member PIN or per-member credential.
