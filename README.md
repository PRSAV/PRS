# PRS.AssetVerify v7

Version 7 adds device GPS capture, configurable Sticky / Variable field masters, live barcode/QR Scan & Verify, and company-specific custom Roles & Permissions.

Frontend target: https://prsav.github.io/PRS/
Worker binding names remain:
- DB -> Cloudflare D1
- Photos -> Cloudflare R2
- OPENAI_API_KEY -> Secret

Important GPS note: browser geolocation records the device latitude/longitude at capture/upload/scan time. For a gallery photo it is the device location when the file is uploaded, not EXIF GPS from the historic photograph.
