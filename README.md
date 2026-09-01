# PRS.AssetVerify Version 10

Version 10 preserves the stable `v8_*` cloud schema and all V9 features, while improving role administration and request reliability.

## V10 changes
- At least one active system Admin is compulsory at all times.
- The last Admin cannot be reassigned to another role or deleted.
- System-generated Admin, Verifier and Viewer roles are editable.
- System roles keep stable internal keys (`ADMIN`, `VERIFIER`, `VIEWER`) even if renamed.
- Role assignment validates the final member-role state before applying updates.
- The active session refreshes when the selected member's role changes.
- Frontend API handling avoids raw `Failed to fetch` messages and provides clearer connectivity errors.
- Existing V9 data, roles, records, photos, backups, PINs, audit trail, offline queue, GPS, scanning and multi-image verification are preserved.

## Data policy
V10 does not reset company data. Future updates should continue migrating the existing stable `v8_*` schema in place.
