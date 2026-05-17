# Firebase Setup

The handbook runs locally without Firebase. Enable Firebase when you want Google sign-in, companion editing, and Firestore sync for trip text data.

## Firebase Console

1. Create a Firebase project.
2. Add a Web App.
3. For local testing, copy `firebase-config.local.example.js` to `firebase-config.local.js` and fill in the Web App config.
4. Do not commit `firebase-config.local.js`; it is ignored by Git.
5. Enable Authentication > Sign-in method > Google.
6. Create Firestore Database.
7. Publish `firestore.rules` to Firestore Rules.
8. Do not enable Storage on the free Spark plan. PDFs, receipts, and photos intentionally stay in local browser storage.

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

## First Owner

The first signed-in user creates the trip member document for themselves. Add travel companions in the site under `設定 > 旅伴共用編輯`.

Firestore text data syncs across signed-in members. Uploaded PDFs, receipts, and photos stay in local browser storage and should be backed up separately.

The current shared trip id is configured in `trip-data.js`:

```js
tripId: "vietnam-2026-da-nang"
```

Use a different `tripId` for future countries or trips.
