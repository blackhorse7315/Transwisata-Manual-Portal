# Transwisata Manual Portal

Operations Manual Studio for PT. Transwisata Prima Aviation, with OM A-D and additional company manuals.

The portal uses assigned username/password accounts. Active members can edit manuals and view cloud revision records. Administrators manage user access and delete or recover revision log entries.

## Latest backend update

Use **firebase-manual-library-update.zip**, extract into a new folder, then follow **MANUAL-LIBRARY-UPDATE.md**. This combined update supports additional manuals AND administrator log deletion/recovery. It deploys 9 Firebase Functions, including portalManageRevisions. Existing accounts and OM snapshots are retained; do not run initial administrator bootstrap again.

## Manual library

Create independent manuals with a short code (CMM, SMS, SEP, etc.) and full name. Choose a standard front-page template, the OM image-document template, or a blank manual. Select or add Front Page, covering letter, DKPPU control image, editable Document Control, automatic LoEP, Record of Revision and automatic Table of Contents. Hidden front pages retain their edits. All manuals are included in backups, shared cloud snapshots, and named revision logs.

## Editing

Word-style ribbon with pin/unpin; direct page editing; automatic typing/paste pagination; independently numbered LoEP, ROR, TOC and content; page layout and paragraph scope; A4/A3/A5/Letter/Legal/Tabloid; portrait/landscape; custom logos/fonts; tables; image wrapping/layers; revision bars; signatures and complete signed approval boxes; undo/redo; fixed panels, fullscreen and keyboard/mouse zoom.

Imported PDF text/layout needs review. Scans require OCR. Manuals and service-account credentials are not included in this repository.
