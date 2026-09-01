# PRS.AssetVerify Version 9

Version 9 keeps the stable cloud data schema used from V8 onward and adds:

- Universal close/exit controls for pages, drawers and modals.
- Delete company directly from Existing Companies after system Admin name + PIN verification.
- Complete company Backup & Restore including photos, members, PIN hashes, roles, masters, records and audit trail.
- Persistent data policy from V9 onward: future upgrades must migrate the existing stable `v8_*` tables in place instead of starting new version tables.
- Multiple-image verification: attach up to 12 camera/gallery images to one verification and scan multiple barcode/QR images/codes.
- Existing V8 offline queue/session storage keys are intentionally retained so local data is not discarded by the V9 frontend update.

## One-time V9 reset
At the user's request, the first V9 Worker request performs a one-time cleanup of all companies that existed before V9 and records `v9_initial_reset_done` in `v8_app_meta`. It never repeats after the marker is written.
