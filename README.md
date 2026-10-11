# Transwisata Manual Portal

Operations Manual Studio for PT. Transwisata Prima Aviation: OM A, B, C and D.

## Current deployment

`index.html` remains the existing application. Login/account management and server-generated revision audit have been prepared in `login-admin-preview.html`; Firebase backend deployment and initial administrator provisioning are pending. The preview will accept login only after backend activation.

See [activation instructions](LOGIN-ACTIVATION.md) and [backend/source package](firebase-login-admin.zip). Do not replace the main application or deploy access rules until the backend and administrator have been verified.

## New version

- Firebase Authentication username/password login.
- Admin-only user management (name, username, password reset and removal of access).
- Shared Log of Revision: editor identity, manual, chapter, page number, added/deleted text, changed fields and server date/time displayed in WIB.
- Server-side role enforcement and conflict-protected cloud commits. No plaintext passwords in public code, Firestore profiles or manual backups.
- Existing Firebase snapshots retained and compatible. Earlier edits have no retroactively invented attribution.

## Existing editor

Portrait/landscape for a page or whole manual; A4/A3/A5/Letter/Legal/Tabloid. Scoped paragraph alignment and spacing, tables with row/column insertion, image wrapping/layers, editable LOEP/TOC, imports, revision bars, signatures, undo/redo, automatic paste pagination, fixed panels, zoom and fullscreen.

Imported PDF text/layout needs review. Scans require OCR. Manuals and service-account credentials are not included in this repository.
