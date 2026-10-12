# Transwisata Manual Portal

Operations Manual Studio for PT. Transwisata Prima Aviation, with OM A-D and additional company manuals.

The portal uses assigned username/password accounts. Active members can edit manuals and view cloud revision records. Administrators manage user access and delete or recover revision log entries.

## Latest backend update

Use **firebase-aircrew-font-update.zip**, extract into a new folder, then double-click **firebase-admin/deploy-update.cmd** or follow **AIRCREW-FONTS-UPDATE.md**. This combined update includes custom manuals, admin log deletion/recovery, the Aircrew read-only role and portalReadManuals. It deploys 10 Firebase Functions in the manual-portal codebase. Existing accounts and manual snapshots remain in use. The script increases the CLI discovery timeout to 60 seconds and the backend initializes Admin services on request.

## Aircrew access and text formatting

Administrators create or edit non-admin accounts as User (editor) or Aircrew (read-only). Aircrew opens a dedicated manual reader with manual/page selection, search, navigation, reading zoom and Refresh. Server permissions reject all Aircrew uploads, manual commits, account management and audit-log operations. The Aircrew option is gated on deployed backend support.

Editors can choose Arial/Calibri and font size for selected text, the current page or all pages in the current manual, with Left/Center/Right/Justify paragraph alignment and undo/redo.

## Manual library

Create independent manuals with a short code (CMM, SMS, SEP, etc.) and full name. Choose a standard front-page template, the OM image-document template, or a blank manual. Select or add Front Page, covering letter, DKPPU control image, editable Document Control, automatic LoEP, Record of Revision and automatic Table of Contents. Hidden front pages retain their edits. All manuals are included in backups, shared cloud snapshots, and named revision logs.

## Editing

Word-style ribbon with pin/unpin; direct page editing; automatic typing/paste pagination; independently numbered LoEP, ROR, TOC and content; page layout and paragraph scope; A4/A3/A5/Letter/Legal/Tabloid; portrait/landscape; custom logos/fonts; tables; image wrapping/layers; revision bars; signatures and complete signed approval boxes; undo/redo; fixed panels, fullscreen and keyboard/mouse zoom.

Imported PDF text/layout needs review. Scans require OCR. Manuals and service-account credentials are not included in this repository.
