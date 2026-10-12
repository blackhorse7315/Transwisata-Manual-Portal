# Arial / Calibri, page formatting scope and Aircrew reader

This combined update includes all existing manual-library and administrator revision-log features, plus a read-only Aircrew role and server workspace reader.

## Activate backend (Windows)

1. Extract firebase-aircrew-font-update.zip into a NEW folder.
2. Open firebase-admin in the extracted folder.
3. Double-click deploy-update.cmd, or open Command Prompt in that folder and run these commands separately:

```bat
npm --prefix functions ci
set "FUNCTIONS_DISCOVERY_TIMEOUT=60"
firebase deploy --only functions:manual-portal --project ecrew-absensi-183ac
```

If firebase is not recognized, install the official CLI with npm install -g firebase-tools. If login is required, run firebase login with the same Google account used for this project.

The backend now contains 10 functions. Confirm portalReadManuals and portalManageRevisions are present and deployment ends with Deploy complete!. Existing accounts, manuals, revision records and project Firestore rules are retained. The script deploys only the manual-portal Functions codebase. Aircrew reads manuals through portalReadManuals with server-side membership checks.

The SDK is initialized when a request arrives instead of during CLI discovery. The discovery timeout is also raised to 60 seconds to address the earlier Timeout after 10000 error. Official guidance: https://firebase.google.com/docs/functions/tips#avoid_deployment_timeouts_during_initialization

## Editing fonts and paragraphs

Refresh the portal with Ctrl + Shift + R, then open the Home ribbon.

- Font family: Arial or Calibri.
- Font size: choose the point size.
- Formatting scope: Selected text / paragraph; Select current page; Select all pages in the current manual.
- Paragraph alignment: Left, Center, Right or Justify.
- Bulk formatting supports undo/redo and leaves other manuals unchanged.
- Header/footer and images retain their existing controls. Generated LoEP/TOC tables adjust their page capacity when the body font size changes. Review text and table fit before printing.
- Calibri is a device font; devices without it use the browser fallback font.

## Creating an Aircrew account

Login as admin -> Manage users -> Add user -> fill name, username and password -> choose Aircrew (read manual only) -> Save user. Existing non-admin accounts can also be changed between User and Aircrew. Protected administrator accounts remain protected.

Aircrew opens a dedicated Manual Library screen with manual selection, page search, Previous/Next, reading zoom and Refresh. It contains no editor, imports, user management, revision-log controls or formatting ribbon. Cloud loading uses the shared workspace and does not upload, create revisions or overwrite device drafts. The server rejects Aircrew uploads, commits, account management and audit-log operations. The Aircrew role option is unavailable until the updated backend reports support.

## Validation

15 backend tests passed, covering active membership, role assignment, role downgrade, forbidden Aircrew writes and account/audit access, read-only snapshot access, staging-upload rejection, additional manuals and log deletion/recovery. Frontend tests passed for current/all-page fonts, right alignment, table fonts, undo/redo, generated-table numbering parity, Aircrew read-only DOM, navigation, no cloud writes, backend-capability gating and device draft isolation. Local SDK discovery finds all 10 functions without initializing Admin services.
