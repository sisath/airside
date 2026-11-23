# CloseBy 1.4

Offline Bluetooth group chats for up to eight nearby people. Any supported iPhone or Android can create or join. Android hosting requires BLE advertising support. One room connects at a time; the owner relays messages and must stay nearby with CloseBy open.

## New in 1.4

- Tap the CloseBy logo in a chat to return to today's chats, keeping the room and its saved history.
- Removed explanatory banners/footer copy. App labels and controls use title case; user-authored text and names are preserved.
- The chat menu contains Show Chat Code, Enable Message Alerts, Clear Messages On This Phone and End Chat, plus the actual app version. Alerts default on for each room, request OS permission and can be turned off. Clear affects only this phone's copy of the current room.
- Tap the group icon to see current connected/available participants.
- Photo, video and voice controls are icon buttons. Tap the heart to send a vibrating heart to the group and open an optional custom-message composer. Sending that message also carries the heart/vibration flag. Tap a heart message to reply. Incoming vibration respects the room's alerts setting and phone vibration settings; offline/suspended delivery still cannot be guaranteed.
- Encrypted room messages, approval, media and original expiry are retained. All participants should update to 1.4 for heart vibration support.

## Features From 1.3

- Real room messages and media survive entering the demo, leaving a room, switching rooms and restarting the app. Room history is encrypted locally with a random per-room key stored in the platform secure store. Fresh Bluetooth keys and approval are still required when reconnecting. Live transport sessions are never restored from disk.
- The original 24-hour deadline remains unchanged. Expired saved rooms and their keys are deleted while running or on next launch/resume. Clear messages deletes this phone's saved copy. Leaving a room preserves it. Copies saved by other people cannot be deleted remotely.
- Record video opens the system camera after camera/microphone permission. Clips are limited to five seconds and 1 MB. Low quality is requested; phones may produce larger files, which are rejected with a request for a shorter clip. MP4 and camera MOV containers are supported. Tap a received/sent video to play it with native controls.
- Bluetooth video transfers can take several minutes. Progress, cancellation and explicit retry are available. Keep everyone nearby and reopen/reconnect after recording if the camera interrupted the Bluetooth session.

## Existing features

Six-character invitation codes such as ABC 123; owner approval with matching verification numbers; today's rooms on the home screen; text, small photos and 15-second voice messages; typing indicators and optional local alerts. Demo participants are S and W. The demo is simulated and is not saved to real room history. Messages lost before this update cannot be recovered.

Photos and voice files remain limited to 64 KB each. Video is limited to 1 MB, total room media to 4 MB, and room packets/messages to 6000. The short code identifies a room and is not an encryption password. Each approved connection uses fresh Noble X25519/HKDF-SHA256 keys and XChaCha20-Poly1305 encryption; compare verification numbers before approval. This custom protocol has software tests but no independent security audit. The owner can read and relay messages.

There are no internet messaging servers, remote push notifications or analytics. Android INTERNET permission is blocked. Fully offline message receipt is not reliable while suspended or closed. Expiry uses phone clocks; cleanup runs when the operating system lets the app run.

## Build and validation

Run npm ci, then npm run check. The suite has 51 tests, including encrypted archive tampering/expiry, restored owner/guest reconnection, media restoration, video bounds, receipt handling and short-code approval. Browser export plus scripts/verify-ui.cjs verifies the preview. Native camera, secure storage, video/audio playback and Bluetooth interoperability require physical-phone testing.

Android is a personal-test ARM64 APK. The GitHub iPhone workflow compiles an unsigned IPA; install with Sideloadly using the same Apple account as before. Update all phones to 1.4 for heart and video support. Bundle/package identifier stays com.airside.privatechat. Repository and IPA filenames retain the legacy Airside name.
