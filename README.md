# Scrum Poker

Live: https://felixhering-debug.github.io/scrum-poker/

Planning poker for agile teams to estimate user stories. No accounts and no own server: a static page (GitHub Pages) plus Firebase Realtime Database for live sync.

## Features
- Create a room, share the link or code, join with a name
- Secret voting: a vote stays in the private area of the database until the cards are revealed
- Reveal by button or automatically when everyone has voted; average, median, distribution, consensus
- Story list with a result per story and a total
- Decks: Fibonacci, modified Fibonacci, T-shirt sizes, powers of two
- Observer mode, light/dark

## Setup (one time, about 10 minutes)

### 1. Create a Firebase project
1. https://console.firebase.google.com → Add project (Analytics can stay off).
2. **Build → Authentication → Get started → Sign-in method → Anonymous → enable.**
3. **Build → Realtime Database → Create database**, pick a location, start in **locked mode**.
4. Tab **Rules**: paste the content of `database.rules.json` and **Publish**.
5. **Project settings (gear) → General → Your apps → Web app (`</>`)**: register an app and copy the `firebaseConfig` block.

### 2. Enter the configuration
Copy the values into `config.js` (including `databaseURL`), commit and push.

### 3. Publish with GitHub Pages
Repo → **Settings → Pages → Deploy from a branch → `main`, folder `/ (root)`**. After about a minute the site is available at `https://<name>.github.io/<repo>/`.

### 4. Authorize the domain
Firebase → **Authentication → Settings → Authorized domains**: add `<name>.github.io`.

## Limits
- Anyone who knows a room code can join and change stories (like the original tools).
- Rooms are not deleted automatically; remove old ones in the Firebase console under Realtime Database → `rooms`.
- Free on the Spark plan, plenty for team sizes.
- Without a configuration the page runs in a demo mode (only tabs in the same browser are synced).

## Try locally
Run `python3 -m http.server 8000` in the folder and open http://localhost:8000 (modules do not load over `file://`).
