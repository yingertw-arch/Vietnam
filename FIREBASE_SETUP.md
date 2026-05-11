# Firebase Setup

The handbook runs locally without Firebase. Enable Firebase when you want Google sign-in, companion editing, cross-device sync, and cloud document storage.

## Firebase Console

1. Create a Firebase project.
2. Add a Web App.
3. For local testing, copy `firebase-config.local.example.js` to `firebase-config.local.js` and fill in the Web App config.
4. Do not commit `firebase-config.local.js`; it is ignored by Git.
5. Enable Authentication > Sign-in method > Google.
6. Create Firestore Database.
7. Publish `firestore.rules` to Firestore Rules.
8. Optional: enable Storage only if you need cloud sync for PDFs, receipts, and photos.
9. Optional: publish `storage.rules` to Storage Rules after Storage is enabled.

## First Owner

The first signed-in user creates the trip member document for themselves. Add travel companions in the site under `設定 > 旅伴共用編輯`.

If Storage is not enabled, Firestore text data still syncs. Uploaded PDFs, receipts, and photos fall back to local browser storage.

The current shared trip id is configured in `trip-data.js`:

```js
tripId: "vietnam-2026-da-nang"
```

Use a different `tripId` for future countries or trips.
