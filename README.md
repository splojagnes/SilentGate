# SilentGate

**Developer:** SplojTech  
**Version:** 1.1.0 (versionCode 2)  
**Package:** `com.silentgate`

SilentGate is a private call blocker **and default phone app**. Only saved contacts
ring. Unsaved, private, and unknown callers are rejected before ringing, logged
locally, optionally synced to Android's native block list, and shown as a clean
SilentGate notification.

Built with Kotlin, Jetpack Compose, MVVM + Clean Architecture, Room,
`CallScreeningService`, and `InCallService`.

## Features

- **Default dialer:** keypad, recents, searchable contacts, dual-SIM labels and
  SIM selection, incoming/active-call screens, mute, speaker, hold, DTMF keypad,
  locked-screen support, and ongoing-call notification.
- **Add call + conference:** during an active call, hold the original, dial a
  second number, then use **Conference** when Android/Telecom and the carrier
  report conference capability. Incoming waiting calls never become conference
  participants.
- **Versioning:** release values live in `version.properties`. `versionCode`
  must increase for every Play upload; `./gradlew bumpVersion` increments the
  patch version and code.
- **Strict screening:** unsaved, private, and restricted callers are rejected
  before the phone rings.
- **Blocked-call notifications:** “Call blocked — `<number>` tried to call and was
  blocked.” Tapping opens the Shield.
- **Shield:** master switch, today/all-time counts, blocked log (one row per
  number), and whitelist.
- **Call back:** permanently whitelists a blocked number and removes its native
  block-list entry. `Add to contacts` opens the contacts editor.
- **Native block list:** Blocked numbers are added via `BlockedNumberContract`
  while SilentGate holds the default Phone role. Settings also has **Sync now**
  and an **Open system blocked numbers** fallback.
- **Call-log cleanup:** rejected call-log entries are removed (with repeated
  retry attempts) and retained only in SilentGate's Room database.
- **Local privacy:** no account, no analytics, no ads, no Internet permission.

## Requirements

- Android Studio with AGP 9.3.x / Gradle 9.5
- JDK 17+ (Studio JBR works)
- Android SDK Platform 37.0
- A phone or emulator with telephony
- Full third-party screening is supported on **Android 10+**. Android 7–9 support
  API 24, but only the default dialer's screening service is invoked on those
  versions.

## Run

```bash
./gradlew :app:assembleDebug
./gradlew :app:installDebug
```

Debug package: `com.silentgate.debug`  
Release package: `com.silentgate`

Onboarding requests:
1. Contacts
2. Call Screening role
3. Default Phone app role
4. Phone access, call log, and notifications

## Upload package

Ready-to-publish files are in:

```
app/build/outputs/apk/UPLOAD/
├── SilentGate-v1.1.0.aab
├── SilentGate-v1.1.0.apk
├── SilentGate-App-Details.txt
├── SilentGate-Privacy-Policy.txt
├── SilentGate-Store-Icon-512.png
├── SilentGate-Feature-Graphic-1024x500.png
├── SHA256SUMS.txt
└── screenshots/
```

The same folder is mirrored at the project root under `UPLOAD/`.

Signing key: `signing/SilentGate-upload.jks`  
Alias: `silentgate`  
Credentials: `keystore.properties` and `signing/README.txt`  
**Back up the keystore and passwords. Never publish them.**

Before uploading, add the official SplojTech support email, host the privacy
policy, and complete Play Console declarations for the default Phone handler,
call log, contacts, Data Safety, and content rating.

## Verify

```bash
./gradlew :app:testDebugUnitTest
./gradlew :app:lintDebug
./gradlew :app:assembleRelease
./gradlew :app:bundleRelease
```

- Blocked-call notifications
- Blocked-call cleanup from the system call log
- Native block-list sync
- Keypad, recents, contacts, Shield, and settings
- Incoming/active call UI on the emulator

## Architecture

```
data/
  call/         CallManager, dialer account provider
  local/        Room database, entities, DAOs
  notification/ Blocked-call and ongoing-call notifications
  repository/   Android implementations
domain/
  model/        Pure Kotlin models
  repository/   Interfaces
  usecase/      Screening, block/unlock, sync, settings
service/        CallScreeningService + InCallService
ui/
  call/         Full-screen incoming/active call UI
  navigation/   Four-tab dialer shell
  screens/      Onboarding, Keypad, Recents, Contacts, Shield, Settings
  theme/        Brand theme
  components/   Shared Compose UI
di/             Manual dependency container
```

## Android limits

`BlockedNumberProvider` normally only permits the system, default Phone app,
default SMS app, and carrier apps to write. SilentGate is designed to be the
default Phone app, which enables native block-list sync. If the role is revoked,
Settings explains the restriction and provides a system screen fallback. Call
screening still works while the Call Screening role is held.
