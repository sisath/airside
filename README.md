# CloseBy 1.2.1

Fully offline Bluetooth rooms for up to eight nearby participants. Any supported iPhone or Android phone can create or join a room. The creator relays messages, so everyone must stay nearby with CloseBy open. Android hosting requires BLE advertising support.

## New in 1.2.1

- Removed suggested snack/outside messages. Demo participants are S and W.
- Voice playback explicitly restores the iOS audio session with silent-mode playback enabled after recording and before playing received memos. Physical iPhone playback still needs verification.
- Today’s chats appear on the home screen, saved on this phone with role, code and original expiry. Reopening uses Bluetooth and owner approval again; only one room can connect at a time. Switching rooms clears the previous in-memory messages. The list contains today’s created/approved joined rooms, not a server membership directory.

## Features from 1.2

- Six-character codes such as `ABC 123`.
- Owner approval for each new connection. Compare the six-digit verification number on both phones before approving; names are self-chosen and are not verified identities.
- Rooms expire 24 hours after creation. The deadline is shared with guests and shown in the chat. The app clears room messages, connection keys, its saved room code and temporary media at expiry while running, or when next opened after suspension. Offline expiry uses the phones' clocks. There is no internet registry reserving codes forever; a later new room can coincidentally use the same short code and gets fresh keys.
- Typing indicators, in-app new-message alerts, and optional local OS notifications for messages actually received over Bluetooth. Enable message alerts in Settings. There are no push tokens, APNs/FCM delivery servers, or reliable delivery while the app is closed/suspended. Notifications omit message contents and media.
- Photos selected through the system picker, re-encoded to JPEG at up to 480 pixels on the longest side. Attachments are limited to 64 KB.
- Mono AAC voice recording and playback, up to 15 seconds, recorded only after tapping Record and granting microphone access.
- Chunked media transfers with progress, cancellation, retry, duplicate suppression, bounded reassembly and SHA-256 integrity checks. Bluetooth transfers can be slow, particularly with many participants. Video and general file sharing are not included.

## Connection privacy

The short code identifies a nearby room; it is not a strong password. Each approved link derives a fresh encryption key using Noble X25519 and HKDF-SHA256, and seals frames with XChaCha20-Poly1305. A verification number derived from the connection transcript is shown on both phones for comparison. Do not approve mismatched numbers. This protocol has software tests but has not had an independent security audit. The owner can read and relay group messages. Room participants can save copies outside CloseBy; those cannot be remotely deleted.

## Testing and installation

Run `npm ci`, then `npm run check`. `npx expo export --platform web` plus `node scripts/verify-ui.cjs` checks the browser demo and create/join screens. The solo demo includes simulated participants and a generated photo illustration; no messages leave the device.

The Android release is a personal-test ARM64 APK. The iPhone GitHub workflow compiles an unsigned IPA on macOS, then Sideloadly signs it locally with the user's Apple account. The bundle/package identifier remains `com.airside.privatechat` for update continuity. Existing repository, archive folder and unsigned IPA filenames retain legacy Airside names. The app display name is CloseBy.

Update every participant to 1.2; the approval/encryption layer and short-code discovery cannot communicate with 1.1 or the original Airside app. Follow INSTALL.md for the physical-phone checklist. Radio interoperability, audio recording/playback, photo picking and local notification behavior must be checked on actual phones before relying on them.
