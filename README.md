# Transwisata Manual Portal

Operations Manual Studio for PT. Transwisata Prima Aviation: OM A, B, C and D.

## Open the application

Open `index.html` locally for editing, or publish it through GitHub Pages:

1. Open repository Settings > Pages.
2. Select Deploy from a branch, branch `main`, folder `/ (root)`.
3. Save and wait for GitHub to show the published address.

The application includes its PDF and DOCX readers. Firebase cloud sync requires an internet connection.

## Firebase

Project: `ecrew-absensi-183ac`.

1. Enable Email/Password in Firebase Authentication and create the intended user account. Google sign-in is optional.
2. Create the default Cloud Firestore database.
3. Add the match block in `firestore-rules-snippet.txt` inside your existing `match /databases/{database}/documents` block. Keep all rules used by your other applications.
4. For Google sign-in, add the published website domain to Authentication > Settings > Authorized domains.
5. Open Cloud Sync, sign in, and choose Upload this device or Load cloud. Automatic sync starts after this first choice.

Cloud data is account-specific under `operationsManualStudio/{uid}`. Another device must use the same account to access the same manuals. Concurrent edits are checked before saving; an outdated device is asked to reload instead of overwriting another device's changes.

The Firebase web configuration is included in the HTML. No service-account credentials are included. Manual contents entered by users are saved locally or to the signed-in user's Firestore workspace, not committed to this repository.

## Features

- Independent OM A–D workspaces and automatic LOEP / table of contents.
- Editable A4 pages, revision bars, signatures and stamps.
- PDF, DOCX, TXT and JSON import; editable PDF text with chapter/header recognition.
- Undo/redo, paragraph formatting, automatic paste pagination.
- Independent panel scrolling, zoom controls, fullscreen editing.
- Desktop Ctrl + scroll up: zoom out; Ctrl + scroll down: zoom in.
- Local offline saving, JSON backups, print / PDF export and Firebase cloud sync.

PDF scans without a text layer need OCR. Review imported layouts before printing.

Firebase Authentication, Firestore access rules and a live cloud connection must be configured and verified in the project before cloud sync can be used.

