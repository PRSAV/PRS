# PRS.AssetVerify v8

Version 8 focuses on field reliability and accountability while retaining the Version 7 GPS, barcode/QR scanning, configurable masters, roles/permissions, AI identification, shared D1/R2 records and Excel export.

## New in Version 8

- **Offline mode + automatic sync**: after the app has been opened online and the user has logged in/selected a member, verification records and edits can be saved locally in IndexedDB when connectivity is lost. Pending items are clearly marked and automatically retried when the device comes back online. Record creation uses a stable client ID so retries do not create duplicate cloud records.
- **Audit Trail**: company activity is recorded server-side in D1, including company login, member selection, member/role/master changes, record creation/edit/deletion, company changes, password reset events and AI identification. The audit trail intentionally does not store passwords, PINs or photo binary data.
- **Member PIN**: every member has a personal 4–6 digit PIN. Company credentials open the company; selecting a member then requires that member's PIN. PIN values are salted/hashed and are never returned by the API.
- **Viewport-safe close controls**: hamburger-menu subviews have a fixed close button and modal headers have sticky close buttons. The app uses `window.visualViewport` plus safe-area insets so the close control stays reachable on phone screens when browser chrome/viewport size changes.

## Existing Version 7 features retained

- GPS latitude, longitude and accuracy stored per verification and exported to Excel.
- Take Photo, Gallery and Scan & Verify (barcode / QR).
- Configurable Sticky and Variable fields under Setting & Master.
- Company-specific Roles & Permissions and custom roles.
- OpenAI photo asset identification.
- Shared metadata in Cloudflare D1 and photos in R2.

Frontend target: `https://prsav.github.io/PRS/`

Worker binding names remain:
- `DB` -> Cloudflare D1 database `pv-capture-db`
- `Photos` -> Cloudflare R2 bucket `pv-capture-photos`
- `OPENAI_API_KEY` -> existing Cloudflare secret

Version 8 uses fresh `v8_*` D1 tables. Version 7 test companies are not automatically migrated into Version 8.

### Offline limitation

A browser/PWA must be loaded successfully online at least once before it can work offline. The user should log in and select their member while online before going into a no-signal area. Switching members requires internet because the PIN is validated by the Worker. AI identification also requires internet; manual asset entry remains available offline.
