# PRS.AssetVerify Version 11

Version 11 is a non-destructive upgrade. Existing companies and their cloud data are preserved.

## V11 fixes and features

- At least one active Admin is compulsory at all times. The last Admin cannot be reassigned or deleted.
- Role assignment is validated and applied safely; errors are returned as readable application messages rather than raw `Failed to fetch` wherever the Worker is reachable.
- System-generated Admin, Verifier and Viewer roles are editable (name, description, permissions and assignments) but cannot be deleted.
- Immutable system-role identities keep Admin logic intact even if a system role is renamed.
- Capture flow is explicit: Sticky Fields → Take/Upload/Scan → Continue to Variable Details → review assets → Save Verification.
- GPS and AI run in the background after the capture review opens, so they do not block progression.
- All V9/V10 features remain: multi-image verification, GPS, barcode/QR scan, offline queue/sync, audit trail, member PIN, dynamic Setting & Master, Excel export, company backup/restore, usage monitoring and R2 photo storage.
- V11 does NOT run any startup routine that deletes companies.

## Persistence rule

V11 continues using the stable `v8_*` D1 tables and migrates them in place. Deploying V11 must not delete existing companies, members, roles, records, audit history or photos. Company/record deletion occurs only when a user explicitly uses a delete action.
