# Firebase Setup

The handbook runs locally without Firebase. Enable Firebase when you want Google sign-in, companion editing, and Firestore sync for trip text data. Files use Google Drive instead of Firebase Storage.

## Firebase Console

1. Create a Firebase project.
2. Add a Web App.
3. For local testing, copy `firebase-config.local.example.js` to `firebase-config.local.js` and fill in the Web App config.
4. Do not commit `firebase-config.local.js`; it is ignored by Git.
5. Enable Authentication > Sign-in method > Google.
6. Create Firestore Database.
7. Publish `firestore.rules` to Firestore Rules.
8. Do not enable Storage on the free Spark plan. PDFs, receipts, and photos upload to Google Drive after the user grants Drive access.
9. In the linked Google Cloud project, enable Google Drive API for Drive uploads.

## GitHub Pages

The repository keeps `firebase-config.js` blank so Firebase config values are not committed to Git history. Firebase Web API keys are public client identifiers, not server secrets, but they still need protected Authentication domains and Firestore rules. The GitHub Pages workflow creates `firebase-config.js` during deployment from repository secrets.

Add these secrets in GitHub repository Settings > Secrets and variables > Actions:

- `FIREBASE_API_KEY`
- `FIREBASE_AUTH_DOMAIN`
- `FIREBASE_PROJECT_ID`
- `FIREBASE_STORAGE_BUCKET`
- `FIREBASE_MESSAGING_SENDER_ID`
- `FIREBASE_APP_ID`
- `FIREBASE_MEASUREMENT_ID`

Then set GitHub Pages source to GitHub Actions. The deployed site will receive Firebase config, while the source branch stays free of API keys.

In Firebase Authentication > Settings > Authorized domains, add:

- `127.0.0.1`
- `yingertw-arch.github.io`

Remove any unused domains before launch.

## Security Rules

The current rules are scoped to this trip only:

```js
tripId: "vietnam-2026-da-nang"
```

Firestore allows only signed-in trip members to read/write trip data. The first signed-in user can initialize this one trip and becomes the owner.

Before publishing, deploy Firestore rules:

```bash
firebase deploy --only firestore:rules
```

Storage rules are kept in the repository for a future Blaze upgrade, but Storage is not enabled for this launch.

## Google Drive Files

The app requests this Google OAuth scope during sign-in:

```text
https://www.googleapis.com/auth/drive.file
```

This lets the app create and manage files it uploads to the signed-in user's Drive. The app creates or reuses a Drive folder named `Vietnam Travel Handbook`, uploads photos/PDFs there, and stores file metadata in Firestore:

- Drive file id
- file name
- MIME type
- web view link
- thumbnail link when Google provides one

After each upload, the app grants `reader` permission to the emails currently listed in the trip companion list. Add companions before uploading files when possible. If Drive upload fails, the app falls back to local browser storage for that file.

## First Owner

The first signed-in user creates the trip member document for themselves. Add travel companions in the site under `設定 > 旅伴共用編輯`.

Firestore text data syncs across signed-in members. Uploaded PDFs, receipts, and photos use Google Drive links when Drive authorization succeeds.

The current shared trip id is configured in `trip-data.js`:

```js
tripId: "vietnam-2026-da-nang"
```

Use a different `tripId` for future countries or trips.
