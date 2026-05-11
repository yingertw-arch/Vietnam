# [Codex] Vietnam Travel Handbook - 2026-05-08
#codex-handoff

- Project path: `C:\Users\HSPS\Documents\New project 3`
- GitHub remote: `https://github.com/yingertw-arch/Vietnam.git`
- Branch: `codex/mobile-trip-mode`
- Latest commit: `e71064c` (`Wire Firebase config for local testing`)
- Draft PR: https://github.com/yingertw-arch/Vietnam/pull/1
- Status: pushed, draft PR open, not yet merged to `main`

## Completed

- Rebuilt the original Vietnam itinerary site into a mobile travel handbook.
- Added `trip-data.js` so future trips can reuse the same template.
- Added `TRAVEL_TEMPLATE.md` and created local Codex skill `travel-handbook`.
- Added mobile itinerary cards with Google Maps links inside itinerary rows only.
- Added place introduction modal, editable lodging per day, and local storage persistence.
- Added expense tracker with category pie chart.
- Added document/ticket upload area for PDFs/images.
- Added lodging document date range flow to update daily hotel names.
- Added simple amount detection from typed receipt/document text or filenames.
- Added journal, photos, voice input, offline map preparation checklist, and companion email list.
- Added Firebase config entry point in `firebase-config.js`.
- Added `firestore.rules`, `storage.rules`, and `FIREBASE_SETUP.md`.
- Firebase project was created and Web App config was filled in.
- Google Authentication was enabled.
- Firestore Database was created and Firestore rules were published.
- Storage was intentionally not enabled because the project is on Spark/free plan. The app now treats Storage as optional and falls back to local storage for PDFs/photos.

## Verification

- Local preview at `http://127.0.0.1:8123/` loaded successfully.
- Main scripts parsed successfully after splitting `trip-data.js` and `firebase-config.js`.
- Itinerary renders and `trip-data.js` config is applied.
- Git branch pushed to GitHub.

## Next

1. On the next computer, clone or open the repo and checkout:
   ```powershell
   git fetch origin
   git checkout codex/mobile-trip-mode
   ```
2. Start a local static server from the project folder:
   ```powershell
   python -m http.server 8123 --bind 127.0.0.1
   ```
3. Open `http://127.0.0.1:8123/`.
4. Test Google login.
5. After login, go to `設定` and confirm it says shared trip mode / logged in.
6. Add a small test expense and confirm it appears after refresh.
7. If Firestore permission fails, inspect Firestore data for:
   - `trips/vietnam-2026-da-nang`
   - `trips/vietnam-2026-da-nang/members/<your-google-email>`
8. Once local Firebase testing is good, merge PR #1 into `main` so GitHub Pages updates.

## Notes

- `firebase-config.js` contains Firebase Web App public config, not a service account secret.
- Storage is not active. Uploaded PDFs/images are local-only until Storage is enabled on Blaze plan.
- `gh auth status` showed the GitHub CLI token is invalid, but `git push` worked through existing Git credentials.
- Obsidian vault was not found under `Documents` or `Desktop`, so this handoff was written into the project as `HANDOFF.md`.
