# Tag Reaper Scout — Phase 1 (UI Wrapper)

This is the barebones native Android wrapper for Tag Reaper Scout.
No hardware SDK yet — this phase only proves the WebView loads and
runs your existing web app fullscreen, standing in for the browser.

## What's in here
- `app/src/main/assets/index.html` — your existing `cattle-tag-scanner.html`,
  copied in as the Scout web app. Replace this file any time you update
  the web app; no Java changes needed.
- `app/src/main/java/.../MainActivity.java` — loads that HTML in a WebView,
  keeps navigation inside the app, and handles the back button sanely.
- `app/src/main/AndroidManifest.xml` — just INTERNET permission, nothing else.
- No login screen, no OAuth — Scout has no direct backend calls yet
  (per project state as of this build), so there's nothing to authenticate.

## Building via GitHub Actions (no Android Studio needed)
This repo includes `.github/workflows/build-apk.yml`. It builds the APK
in the cloud every time you push to `main`, or any time you trigger it
manually. Nothing about the app itself changes — this just replaces
"build it on your laptop" with "build it on GitHub's servers."

1. Push this whole folder to a new GitHub repo (e.g. `tag-reaper-scout`).
2. Go to the repo's **Actions** tab. You should see "Build Tag Reaper Scout APK"
   run automatically on the push (or click **Run workflow** to trigger it by hand).
3. Wait for the green checkmark (first run takes a few minutes — it's
   downloading the Android SDK and Gradle).
4. Click into the finished run → scroll to **Artifacts** →
   download `tag-reaper-scout-debug-apk`. That's a zip containing `app-debug.apk`.
5. Get that APK onto the C316H (email it to yourself, USB transfer, or
   a file-sharing link) and install it — you'll need to allow
   "install from unknown sources" the first time, since it's not from
   the Play Store.

No Android Studio, no local Gradle, no SDK setup on your end — GitHub's
runner does all of that. You only touch the repo and the Actions tab.

## Alternative: opening it in Android Studio directly
If you ever do want to run it locally instead:
1. Install Android Studio: https://developer.android.com/studio
2. Open Android Studio → "Open" → select this `TagReaperScout` folder.
3. Let Gradle sync (needs internet the first time).
4. Plug in the Chainway C316H (or any Android device) via USB with USB debugging on.
5. Click the green ▶ Run button. Select your device. It installs and launches.

## What "done" looks like for Phase 1
- App installs and opens without crashing.
- The Scout UI renders and behaves exactly like it does in Chrome.
- Pasture input, tag entry, table, tabs, toasts — all work as normal.
- Back button navigates the web app instead of instantly closing the app.

## What's intentionally NOT in this phase
- No Chainway `.aar` SDK.
- No UHF/BLE tag reading.
- No Google Sheets / Gateway sync (Scout doesn't call any backend yet).

Once this is confirmed solid on the actual C316H hardware, Phase 2 wires in
the Chainway SDK and the hardware→JavaScript bridge — a separate, isolated
step so if something breaks, you know exactly which layer caused it.
