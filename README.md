# CloseBy

Offline Bluetooth group text chat. Choose **Create a chat** to generate a code, or **Join a chat** to enter an existing code. Either iPhone or Android can act as the room owner or joiner; Android hosting requires BLE advertising support.

The owner relays messages to a maximum of seven guests (eight people total). Everyone must remain near the owner with Bluetooth on and the app open. There is no automatic owner transfer, internet fallback, background notification service, or earlier-history download for late joiners. Actual simultaneous connection limits depend on the phones.

## Privacy and delivery

The random 20-character invitation code has 100 bits of entropy. Discovery IDs and encryption keys use separate versioned domains. Room packets use XChaCha20-Poly1305 with fresh random nonces and per-connection challenge responses. Names are self-chosen, not verified identities; anyone with the invitation code can join and read the room. The owner can read and relay messages. This is shared-code room encryption, not protection against another room member.

A message becomes Delivered only after every participant present when the owner accepted it acknowledges receipt. Queued/sending/retry states avoid treating a successful Bluetooth write as delivery. Retries suppress duplicates. Messages remain in memory, with a 1000-message session limit; the name, code and last role are saved in secure device storage.

## Build and test

Run `npm ci`, then `npm run check`. `npx expo export --platform web` and `node scripts/verify-ui.cjs` verify the three-person demo and create/join screens. Browser tests simulate the room protocol, not Bluetooth radios.

The native Swift and Kotlin implementations are in `modules/airside-bluetooth`. Both platforms implement BLE peripheral hosting and central joining. Native identifiers and storage keys retain their original Airside names so updates retain the same application identity.

The GitHub workflow prebuilds the iOS project and runs `scripts/build-ios-unsigned.sh` on macOS. The unsigned output retains the legacy filename `Airside-unsigned.ipa` for compatibility with the existing repository workflow; the app's display name is CloseBy. Sign it on Windows with Sideloadly using the same Apple account as the installed app. Use the same bundle identifier override, if one was chosen previously.

The new room protocol is incompatible with the original two-person Airside build. Update every participant's app. Test iPhone→iPhone, iPhone→Android, Android→iPhone and Android→Android on physical phones before relying on the app while travelling.
