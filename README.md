# YouTube (educational Android client)

A fast, ad-free, Compose-based video client for Android. Educational project.

**Stack:** Kotlin, Jetpack Compose (Material 3), Media3/ExoPlayer (Google's player), [NewPipeExtractor](https://github.com/TeamNewPipe/NewPipeExtractor) for data, Coil, R8-shrunk release build.

**Features:** trending + category chips, search with live suggestions and history, watch page with quality picker (up to the best available), speed control, double-tap seek, fullscreen, picture-in-picture, background audio with notification/lock-screen controls, live streams (HLS), comments, related videos + autoplay, channels, subscriptions feed, likes, watch later, watch history, mini player, opens youtube.com / youtu.be links. Subscriptions and library are stored on-device (no account).

## Build

Push to `main` (or run the workflow manually) and download the APK from **Actions -> Build signed APK -> Artifacts**. Tagging `v1.0.1` also attaches the APK to a GitHub Release.

### Stable signing key (recommended)
Without secrets the workflow signs with a throwaway key, so new builds can't update old installs. To keep one identity:

```bash
keytool -genkeypair -v -keystore release.jks -alias tube -keyalg RSA -keysize 2048 -validity 10000
base64 -w0 release.jks   # paste into the KEYSTORE_BASE64 secret
```
Repo -> Settings -> Secrets and variables -> Actions: `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`.

### Local build
Open in Android Studio (Ladybug or newer), or run `gradle wrapper --gradle-version 8.9` once and then `./gradlew assembleRelease`.

## If videos stop loading
YouTube changes its internals often. Bump `extractorVersion` in `app/build.gradle.kts` to the latest tag from the NewPipeExtractor releases page. If the release build crashes, set `isMinifyEnabled = false` to rule out R8.

## Notes
Unofficial. It scrapes YouTube the way NewPipe does, which is outside YouTube's Terms of Service, so keep it personal/educational, and use your own name and icon before sharing it anywhere.
