# House Hunt Scorecard

A weighted scorecard for comparing houses. Two people rate 21 criteria from 1 to 10, the ratings are averaged, weighted by priority, and turned into a score from 1 to 100.

Everything lives in `index.html`, with no build step.

## Scoring

- Each criterion has a priority from 1 (must-have) to 5 (nice-to-have). Priority 1 counts 5× and priority 5 counts 1×.
- Each criterion's score is the average of both people's ratings. If only one person has rated it, that rating is used.
- Weighted average (1–10) → score: `1 + (avg − 1) × 99 / 9`, so all 1s = 1 and all 10s = 100.
- Unrated criteria are skipped. Each card shows how many of the 42 ratings are filled in.

## Sync (Firebase)

When `FIREBASE_CONFIG` at the top of the script in `index.html` is filled in, the page asks for a Google sign-in and syncs houses, priorities and names live through Firestore. Only the accounts listed in `firestore.rules` can read or write. Each rating is saved as its own field, so two people rating the same house at once don't overwrite each other. Firestore's offline cache keeps the page working without signal, and changes sync once you're back online.

If `apiKey` is left empty, the page saves to the browser's `localStorage` instead. To move houses between devices in that mode, use the share link or JSON backup under **Names & data**.

### One-time setup

1. Go to [console.firebase.google.com](https://console.firebase.google.com) → **Create a project**. Google Analytics can be turned off.
2. **Build → Authentication → Get started → Sign-in method → Google → Enable**, then save.
3. In the same section, open **Settings → Authorized domains → Add domain** and enter `jimmybuffett.github.io`.
4. **Build → Firestore Database → Create database**. Pick a nearby location and start in **production mode**.
5. In Firestore, open **Rules**, paste in `firestore.rules` with both Google addresses filled in, and click **Publish**.
6. Open **Project settings** (gear icon) → **General → Your apps → Web (`</>`)** and register an app. Skip Firebase Hosting. Copy the `firebaseConfig` values into `FIREBASE_CONFIG` in `index.html`.
7. Commit and push.

The Firebase web config is safe to commit. It identifies the project, and the security rules control who can access the data.

## Hosting

Served by GitHub Pages from the `main` branch root.
