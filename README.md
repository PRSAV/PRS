# PRS.AssetVerify Version 12

Version 12 is a non-destructive upgrade. Deploying it does **not** delete existing companies, members, roles, verification records, audit history, or R2 photos.

V12 changes:
- Automatic high-accuracy GPS detection starts after Photo / Gallery / Scan evidence is prepared.
- Latitude, Longitude and GPS Accuracy are optional. Denying location or leaving them blank never blocks Save Verification.
- Photo viewing is resilient for authorised users who can view verification records or export reports, including existing roles created before V12.
- Photo URLs are refreshed with the current company session so cached/stale access tokens do not break images.
- Excel export fetches photos with the current authenticated session and embeds the image bytes directly into the workbook.
- Existing V10/V11 compulsory-Admin, editable system-role, multi-image, offline queue, backup/restore and audit features are retained.

Deployment order: Cloudflare Worker first, then GitHub frontend files. See V12_SETUP.md.
