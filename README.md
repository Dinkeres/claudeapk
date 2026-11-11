# kasierWatch – Android

Your `kasierWatch.html` is in `app/src/main/assets/index.html`, byte-for-byte unchanged.
The app is a full-screen WebView that serves that page.

## Build the APK

### Option A: GitHub (nothing to install)
1. Create a new GitHub repository and upload everything in this folder, including the hidden `.github` folder.
2. Open the **Actions** tab. The "Build APK" workflow runs on every push. You can also start it with **Run workflow**.
3. When it finishes (about 3–5 minutes), open the run and download **kasierWatch-apk**. Unzip it to get `app-release.apk`.

### Option B: Android Studio
1. Open this folder in Android Studio (Ladybug or newer) and let it sync.
2. Choose **Build → Build App Bundle(s) / APK(s) → Build APK(s)**.
3. The APK is written to `app/build/outputs/apk/`.

### Option C: Command line
Requires JDK 17+, the Android SDK (with `ANDROID_HOME` set) and Gradle 8.9 or newer:
```
gradle assembleRelease
```

## Installing
Copy the APK to your phone, open it, and allow "Install unknown apps" when Android asks.
The APK is signed with the Android **debug** key. That's fine for sideloading. Use your own keystore if you plan to publish the app.

## What the wrapper adds (the HTML itself is not changed)
- localStorage persists: watchlist, "Prefer no ads", server choice and TMDB IDs.
- The player fullscreen button switches to landscape, immersive fullscreen.
- Back button: exits fullscreen, then closes the open title, then goes back, then quits.
- IMDb, JustWatch and TMDB links open in your phone's browser.
- Embedded players can't send the whole app to another site, and can't open pop-up windows.
  To allow more hosts to open externally, edit `EXTERNAL_LINK_HOSTS` in `MainActivity.java`.

## Updating the page
Replace `app/src/main/assets/index.html` and build again. If you want to use a TMDB key, set `TMDB_API_KEY` in that file before building.
