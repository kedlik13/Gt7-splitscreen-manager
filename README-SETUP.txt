GT7 RACE NIGHT CHAMPIONSHIP MANAGER — INSTALLATION

FILES
- index.html: the app
- sw.js: offline cache service worker
- manifest.json: Home Screen installation metadata
- icon-192.png / icon-512.png: app icons

IMPORTANT
The app works offline after it has been opened online once from its HTTPS website and added to the iPhone Home Screen. GitHub Pages is a free HTTPS host. Opening index.html directly from Files is useful for a quick test, but it does not install the service worker or provide reliable offline Home Screen behaviour.

GITHUB PAGES (iPhone)
1. Sign in to github.com in Safari.
2. Create a new public repository named gt7-race-night.
3. Open the repository and choose Add file > Upload files.
4. In the iPhone Files app, extract this ZIP. Upload all five files from the extracted folder (not the folder itself).
5. Commit the upload.
6. In the repository, open Settings > Pages.
7. Under Build and deployment, choose Deploy from a branch; select main and /(root), then Save.
8. Wait for GitHub Pages to publish. Open the published HTTPS address in Safari.
9. Open the app once while online. Use Share > Add to Home Screen. Launch it from the new Home Screen icon.
10. Test once with Airplane Mode on. Do not delete Safari website data after installation unless you are prepared to reinstall/cache again.

OPTIONAL LIVE SYNC (Firebase free tier)
Both phones need internet when syncing, but they can continue recording races offline. Changes sync automatically when a connection returns. The app uses Firebase Realtime Database REST and anonymous authentication; it does not need a Firebase JavaScript library.

Create a Firebase project:
1. Go to https://console.firebase.google.com/ and create a project.
2. In Project settings, add a Web app and copy its Web API key.
3. In Authentication > Sign-in method, enable Anonymous.
4. In Build > Realtime Database, create a database. Copy its database URL exactly (it looks like https://YOUR-PROJECT-default-rtdb.REGION.firebasedatabase.app).
5. In Realtime Database > Rules, use the rules below, then Publish:

{
  "rules": {
    "rooms": {
      "$room": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}

6. Open GT7 Race Night > Sync on your hosted app. Enter the Web API key and Realtime Database URL, then Save Firebase Settings.
7. On the main phone, tap Create Room & Share Code. Send the 12-character room code to your friend.
8. On your friend's phone, open the same hosted app, enter the same Firebase API key and database URL, save them, enter the room code and tap Join Championship.

SYNC SECURITY NOTE
These rules require an anonymous Firebase sign-in, and the room code acts as the joining key. Anyone who obtains a room code can read or change that room's race data. Use this for non-sensitive game results only, and share the code privately. This is a lightweight friends' scoreboard, not a secure private-data system.

SYNC BEHAVIOUR
- Local saves happen first and work offline.
- When online, the app checks the shared room about every 7 seconds and uploads local changes.
- If both people change data at exactly the same time, the most recently updated whole championship copy wins. For best results, have one person enter race results and let the other phone view the standings.

FEATURES IN THIS BUILD
- Standard and Split Screen race formats.
- 1–4 tournament participants (choose how many before starting; first N drivers in the roster participate).
- Split Screen rain presets only on GT7 layouts that support rain; other layouts use dry/cloudy conditions.
- Split Screen hides fastest-lap entry and bonus.
- Record the actual car used for each player in each race result.
- Standard Championship: under 3.5 km = 1–3 laps; 3.5 km and above = 4–6 laps.
- Endurance Championship: 8–15 laps, independent of track length.
- Custom Laps toggle: OFF randomises within the correct range; ON exposes a slider on the generated race card.
- Track-repeat prevention in a season, standings, statistics, history and local persistence.
