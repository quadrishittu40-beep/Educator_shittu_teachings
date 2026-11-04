# Educator's Desk — Firebase Cloud Backup Edition

Static, GitHub Pages-compatible teacher workspace for Educator Shittu Quadri Adeshina.

## Included
- Existing dashboard, 45 subject/class workspaces and teaching tools.
- Teacher profile with portrait; profile navigation and save behaviour repaired.
- Firebase Authentication (Email/Password) sign-in and account creation.
- Cloud Firestore manual backup and restore.
- Debounced automatic cloud backup after local data changes while signed in.
- Existing local JSON backup/restore retained.
- App icons, favicon and web manifest.

## Publish
Upload the contents of this ZIP to the root of your GitHub Pages repository. Keep the `assets` folder and `manifest.webmanifest` beside `index.html`.

## First use
1. Open the published site using HTTPS.
2. Open **Firebase Cloud Backup** in the left navigation.
3. Sign in with the email/password user already created in Firebase Authentication.
4. Choose **Back Up Now** for the first cloud backup. Automatic backups are attempted after later changes while signed in.
5. Use **Restore from Cloud** to restore the latest backup on another browser/device. Download a local JSON backup before restoring.

## Firebase configuration and security
The Firebase web app configuration is embedded in `index.html` and is intended for browser use. Firebase web API keys are not server secrets; security must be enforced by Authentication and Firestore Security Rules.

The app writes one document at `users/{authenticated-uid}/backups/latest`. The Firestore rules must allow an authenticated user to read/write only their own `users/{uid}/backups/{backupId}` documents. The owner UID configured in Firebase Authentication must match the signed-in account. Never publish service-account private keys or Admin SDK credentials in this static app.

## Important limitations
- Cloud backup is one Firestore document and the app stops before upload if the serialized data is approximately 900 KB or larger. For larger datasets, use a future chunked backup implementation.
- Automatic backup requires an active internet connection and a signed-in Firebase user. If offline or signed out, changes remain in this browser's local storage; use **Backup Data** to download a JSON copy.
- Browser local storage is device/browser-specific. Cloud restore is the method for transferring records to another device.
- Test a manual backup and restore with sample data before relying on it for important academic records.
