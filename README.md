APP IDENTITY
------------
App name:            SilentGate
Developer:           SplojTech
Version name:        1.3.0
Version code:        4
Package name:        com.silentgate
App type:            Android application
Category:            Communication
Suggested rating:    Everyone / 13+ (complete the Play content rating questionnaire)
Primary language:    English
Ads:                 None
In-app purchases:    None

RELEASE FILES
-------------
SilentGate-v1.3.0.aab                    Google Play App Bundle (upload this)
SilentGate-v1.3.0.apk                    Signed release APK (install/testing)
SilentGate-Store-Icon-512.png             512 × 512 Play Store icon
SilentGate-Feature-Graphic-1024x500.png   Play Store feature graphic
SilentGate-Privacy-Policy.txt             Privacy policy text (host online)
screenshots/                              Phone screenshots (1080 × 2400)
SHA256SUMS.txt                            Release file checksums

TECHNICAL
---------
Minimum Android:     7.0 (API 24)
Target Android:      17 (API 37)
Compile SDK:         37.0
Language:            Kotlin
UI:                  Jetpack Compose
Architecture:        MVVM + Clean Architecture
Local database:      Room
Signing:             Signed release APK and AAB
Keystore:            signing/SilentGate-upload.jks
Key alias:           silentgate
Credentials:         keystore.properties and signing/README.txt
                     Keep the keystore and passwords private and backed up.

SHORT DESCRIPTION (80 characters max)
-------------------------------------
A private call blocker and dialer. Only your saved contacts ring.

FULL DESCRIPTION
----------------
SilentGate is a private call blocker and complete phone app with one simple
rule: only saved contacts ring.

Every incoming call is checked against your contacts before the phone rings.
Unsaved, private, and unknown callers are rejected, logged privately, and kept
out. Saved contacts ring normally through SilentGate's own incoming call screen.

SilentGate replaces your phone app with a clean dialer:
• T9 smart keypad: type a name's digits and matching contacts appear
• Favorites / quick dial at the top of Contacts
• Contact profiles with photo, Call, Message, Send image, Favorite and Block
• Recents search plus swipe right to call and swipe left to message
• A distinct SilentGate incoming and active-call screen
• Mute, speaker, keypad (DTMF), hold, and end-call controls
• Locked-screen incoming-call support
• SIM labels on calls
• Add call → original call on hold → Conference (only when your carrier supports it)
• Incoming waiting calls never become conference participants
• Recents and Contacts action menu: Call, Message, Send image
• System ringtone and vibration play through SilentGate incoming calls
• Saved contacts are cleared from stale native block-list entries

THE SHIELD
• Master on/off switch
• Today and all-time blocked-caller counts
• Blocked log with one row per number; repeat calls update the latest time
• Whitelist for numbers you intentionally let through
• Tap a blocked number to call back, permanently unlock it, or add it to contacts
• Silent blocked-call notifications with a daily summary; tap opens the blocked log
• Blocking rules: exact numbers, prefix/wildcards, private callers, per SIM
• Native Android block-list sync when SilentGate is the default Phone app
• Encrypted local backup and restore (AES-256-GCM, password-derived key)
• App lock using device biometric / screen-lock PIN; notification details hidden on lock screen
• Per-SIM ringtone and vibration; custom contact ringtones
• Do Not Disturb, silent, vibrate and ring-volume handled by the incoming call ringer
• Full-screen incoming-call notification fallback for locked/background cases

PRIVACY
• No account, ads, tracking, or analytics
• No INTERNET permission: app data never leaves the device
• Contacts and call log are used only for screening, caller names, recents,
  and call-log cleanup
• Blocked and whitelisted numbers are stored in SilentGate's local Room database
• Blocked call entries are removed from the device call log and kept only
  inside SilentGate

ANDROID ROLES
-------------
SilentGate needs:
1. Contacts permission
2. Call Screening role — reject calls before ringing
3. Default Phone app / Dialer role — SilentGate dialer and call UI
4. Phone and call-log permissions
5. Notification permission (Android 13+)

Android 7–9 only allow third-party CallScreeningService when the app is the
default dialer. SilentGate supports API 24, but the full third-party screening
experience is designed for Android 10 and newer.

PERMISSIONS AND USE
-------------------
READ_CONTACTS        Match incoming numbers with saved contacts.
READ_CALL_LOG        Show recents and find blocked-call entries.
WRITE_CALL_LOG       Remove rejected call entries from the phone call log.
CALL_PHONE           Place calls from the SilentGate dialer.
READ_PHONE_STATE     Read call and SIM state for the phone UI.
ANSWER_PHONE_CALLS   Answer calls through the default Phone role.
POST_NOTIFICATIONS   Show blocked-call and ongoing-call alerts.

PLAY CONSOLE DECLARATIONS
-------------------------
• Default Phone handler declaration and eligibility form.
• Call log permission declaration (core default-dialer functionality).
• Contacts permission declaration.
• Data Safety: no data collected or shared; all processing is on-device.
• Privacy policy URL (required because of sensitive permissions).
• App access: no login; users grant roles and permissions during onboarding.
• Support email: add the official SplojTech support email in Play Console.

SUGGESTED DATA SAFETY ANSWERS
-----------------------------
Data collected:              None
Data shared:                 None
Processed on-device:         Contacts, phone numbers, call history
Encryption in transit:       Not applicable (no data leaves the device)
Data deletion:               Clear app storage or uninstall
Tracking / advertising:      None

TESTING NOTES
-------------
1. Install SilentGate-v1.3.0.apk on a phone with a SIM.
2. Complete onboarding and grant all four setup steps.
3. Call from a number not saved in contacts.
   Expected: no ring; "Call blocked" notification; row in Shield → Blocked.
4. Tap the blocked row → Call back.
   Expected: number is whitelisted and the system block-list entry is removed.
5. Call again from that number.
   Expected: the SilentGate incoming-call screen rings.
6. Check Keypad, Recents, Contacts, and Shield.
7. Settings → Sync now verifies the native Android block list.

VERSIONING POLICY
-----------------
Release versions are read from version.properties.
• versionCode must increase for every Play upload.
• versionName follows patch/minor/major release changes.
• Current: 1.3.0 (versionCode 4)
• Run ./gradlew bumpVersion before the next delivered upload, or edit
  VERSION_NAME/VERSION_CODE manually (major/minor changes).

RELEASE NOTES — 1.3.0
---------------------
• T9 smart dialer and favorite quick dial
• Contact profiles with photo, actions, favorites and blocking
• Recents search and swipe actions
• Exact / prefix / private / per-SIM blocking rules
• App lock with biometric or device PIN
• AES-256-GCM encrypted local backup and restore
• DND-aware ringtone, per-SIM ringtone/vibration, custom contact ringtones
• Full-screen incoming-call notification fallback
• Silent blocked-call notifications with daily summary
• Emergency-number bypass and battery-optimization guidance

RELEASE NOTES — 1.2.0
---------------------
• Fixed incoming calls from saved contacts not ringing: SilentGate now plays
  the system ringtone and vibration while Telecom reports a ringing call
• Added native block-list reconciliation so saved contacts are not kept blocked
• Master toggle and native Sync now skip numbers saved in Contacts
• Recents and Contacts now have Call / Message / Send image actions
• Add call, Swap, and carrier-gated Conference remain available

RELEASE NOTES — 1.1.0
---------------------
• Add call during an active call, with the original call automatically held
• Conference action when Android/Telecom and the carrier report support
• Incoming call-waiting calls are never conference-eligible
• Swap between active and held calls
• Conference UI with participant count and End conference
• Silent blocked-call notifications
• Refined keypad layout, Add to contacts action, and quieter dial UI

RELEASE NOTES — 1.0.0
---------------------
Initial public release.
• SilentGate call screening and local blocked-call log
• Blocked-call notifications
• Full default-dialer experience: keypad, recents, contacts, call screens
• Permanent whitelist via call-back
• Native Android block-list sync
• Dual-SIM account labels and SIM selection
• Developer: SplojTech

REAL-DEVICE TESTING
-------------------
The emulator verification covers the core screening, dialer, ringing, actions,
rules, and UI flows. The following physical-device matrix MUST still be completed
before Play Store release because default-dialer and ringtone behavior varies:
• Samsung (One UI) — Android 13/14/15
• Xiaomi / Redmi (HyperOS) — Android 13/14/15
• OPPO / realme (ColorOS) — Android 13/14/15
• vivo (Funtouch OS) — Android 13/14/15
• Infinix / Tecno — Android 12/13/14
Test: contact call ringing in normal/vibrate/silent/DND, private caller rejection,
unsaved caller rejection, call waiting, Add call/Conference on a carrier that
supports it, dual-SIM switching, call-log cleanup, native block-list sync,
default-role revocation, emergency calls, app lock, lock-screen notification
privacy, and backup/restore.

PLAY STORE EXTERNAL ITEMS
-------------------------
• Support email: add the official SplojTech support email in Play Console.
• Privacy policy URL: host SilentGate-Privacy-Policy.txt and paste the public URL.
• Complete the default Phone handler, call log, contacts, Data Safety, content
  rating, ads, and app-access declarations in Play Console.
These require account-specific information and cannot be completed in this
project package.

Copyright 2026 SplojTech. All rights reserved.
