# Transwisata Manual Portal

Operations Manual Studio for PT. Transwisata Prima Aviation: OM A, B, C and D.

## Run

Open index.html locally, or enable GitHub Pages in repository Settings > Pages, branch main, folder / (root).

## Shared Firebase workspace — no login screen

Project: ecrew-absensi-183ac.

1. Enable Anonymous sign-in in Firebase Authentication.
2. Create the default Cloud Firestore database.
3. Add firestore-rules-snippet.txt inside your existing match /databases/{database}/documents block. Keep rules for the project's other applications.
4. Open the application. Firebase creates an anonymous session automatically, loads the shared OM A–D and enables automatic sync.

All devices use operationsManualPortal/transwisata. Anyone opening the portal can read and edit the shared manuals once these rules are enabled. Individual accounts are not required. Previous account-specific workspaces are left in their original collection and are not migrated automatically.

Local editing remains available offline. Device copies are retained before automatic cloud loads and can be restored through Cloud Sync with automatic sync paused. Cloud transactions reject outdated saves. Download a JSON backup before major changes.

## Features

Editable A4 pages, LOEP and TOC, PDF/DOCX/TXT/JSON import, automatic chapter and title detection, nested numbering, revision bars, signatures and stamps, undo/redo, paragraph formatting, automatic paste pagination, independent panel scrolling, zoom, fullscreen, print/PDF export and a Transwisata application logo.

Desktop Ctrl + scroll up: zoom out; Ctrl + scroll down: zoom in.

PDF scans require OCR. Review converted layouts before printing.

Firebase service-account credentials and user-entered manuals are not committed to this repository. The cloud integration cannot save until Anonymous Authentication and Firestore rules have been enabled in the Firebase project.
