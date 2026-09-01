# PRS.AssetVerify Version 8 deployment

## 1. Deploy the Version 8 Cloudflare Worker

1. Open Cloudflare -> Workers & Pages -> `pv-capture-ai` -> **Edit code**.
2. Replace the entire existing Worker with `cloudflare-worker/worker.js` from this package.
3. Click **Deploy**.
4. Keep the existing bindings unchanged:
   - `DB` -> `pv-capture-db`
   - `Photos` -> `pv-capture-photos`
   - `OPENAI_API_KEY` -> existing secret
5. Click **Visit**. The JSON health response must say `PRS.AssetVerify v8`, `version: 8`, and show database/photo/OpenAI as `true`.

`recoveryEmailConfigured:false` is still expected until reset-email delivery is separately configured.

## 2. Deploy the Version 8 GitHub frontend

In repository `PRSAV/PRS`, replace these files at the repository root:

- `index.html`
- `app.js`
- `styles.css`
- `manifest.webmanifest`
- `sw.js`
- `icon.svg`

Commit to `main`. Keep GitHub Pages on `main` / `(root)`. Wait for the Pages Action to turn green, then open:

`https://prsav.github.io/PRS/`

Use `Ctrl + Shift + R` once on desktop after deployment so an older service-worker cache is not used.

## 3. Version 8 starts with fresh tables

Version 8 uses `v8_*` D1 tables. Existing Version 7 companies will not appear automatically. Create a fresh Version 8 test company. Every team member must receive a **4–6 digit Member PIN**.

## 4. Test Member PIN

1. Create a company while online.
2. Add at least one Admin and one Verifier, each with a different 4–6 digit PIN.
3. Log in with the shared company username/password.
4. Select a team member.
5. Confirm the app asks for that member's PIN before entering the workspace.
6. In Users & Rights, confirm an Admin can add a member with a PIN and can optionally change an existing member PIN.

Do not share actual company passwords or PINs in ChatGPT screenshots/messages.

## 5. Test Offline Mode + Automatic Sync

1. While online, log in and select a member. Let the app fully load once.
2. Reload once while online so the service worker controls the page.
3. Disconnect the device from the internet / use airplane mode.
4. Take a photo or use an already available camera flow and save a verification record.
5. The record should remain visible with **Pending cloud sync**, and the top badge should show **Offline** or a pending count.
6. Reconnect to the internet.
7. The app automatically syncs the queued record. The pending marker should disappear after refresh and the record should exist in D1/R2.
8. Repeat once with an offline edit and once with an offline delete.

Notes:
- Switching members while offline is intentionally blocked because the PIN must be validated by the server.
- AI asset identification needs internet. Manual asset entry works offline.
- A first-ever visit cannot work offline because the browser has not yet cached the application.

## 6. Test Audit Trail

As an Admin open hamburger menu -> **Audit Trail**. Perform a few actions, such as create/edit a verification, add a member, or edit a master field, then refresh Audit Trail. It should show the action, actor, date/time and safe before/after details where relevant.

The trail does not store plaintext company passwords, member PINs, or image binary data.

## 7. Test viewport-safe close buttons

On a phone:

1. Open hamburger -> Search & Filters / Users & Rights / Roles & Permissions / Setting & Master / Audit Trail / Usage.
2. Rotate the phone and change browser viewport height if possible.
3. Confirm the round **X** remains inside the visible screen and returns to Verification.
4. Open a long modal and scroll down. Its header/close button should remain sticky and tappable.

## 8. GPS permission

For GPS capture, allow browser location access. On iPhone/Safari use **While Using** and enable **Precise Location** when appropriate. Latitude/longitude are device-reported coordinates and GPS accuracy is retained as evidence; no browser can guarantee mathematically exact GPS.
