# Install Airside on an iPhone for free, using Windows

This route uses a free GitHub cloud Mac to compile an unsigned device IPA, then a Windows sideloading tool to sign it with your own free Apple account. No paid Apple Developer membership or Expo account is required for this route. The unsigned IPA alone cannot install: the local signing step is essential.

## 1. Build the IPA

The source contains `.github/workflows/ios-unsigned.yml`. In the GitHub repository, open **Actions > Build iPhone app (free sideload) > Run workflow**. It uses the standard `macos-26` runner. Standard runners are free for public repositories; your app source is public with that choice. Private repositories instead draw from the account's included usage and may incur charges beyond that allowance. Do not select a paid larger runner.

The workflow checks the app, generates the iOS project with Expo, installs its native dependencies, and builds a Release application for a physical iPhone without requesting Apple signing credentials. No Apple account or password belongs in this workflow or in GitHub secrets. There are no signing secrets to configure.

When the workflow succeeds, open its run and download the **Airside-iPhone-unsigned** artifact. Extract the ZIP and locate **Airside-unsigned.ipa**. An artifact download may require signing into GitHub. Artifacts are kept for seven days; rerun the workflow if the download expires. The IPA is not an iOS Simulator application.

If the workflow fails, it does not produce a usable IPA. Open the failed step or download the diagnostics artifact so the actual compiler error can be fixed. A workflow file by itself is not proof that the app has built.

## 2. Install from Windows

1. Download Sideloadly only from its official site: https://sideloadly.io/ . It is a third-party tool, not an Apple product.
2. Follow its current Windows prerequisites. Its documentation currently calls for the desktop/web versions of Apple's iTunes and iCloud; use the links from the official Sideloadly site.
3. Connect the iPhone to Windows by USB, unlock it, and tap **Trust** when asked.
4. Open Sideloadly, select the iPhone, and choose **Airside-unsigned.ipa**.
5. Enter your own Apple account in Sideloadly and follow its authentication prompts. Do not send your password or two-factor code in this chat or put them into GitHub. You can use a dedicated free Apple account if you prefer.
6. Start installation. Sideloadly obtains a personal provisioning profile, signs the app, and installs it on the connected iPhone.
7. If iOS requests it, trust your developer profile in **Settings > General > VPN & Device Management**. Enable **Settings > Privacy & Security > Developer Mode** if prompted, restart, and confirm the setting.
8. Open Airside. Tap **Try the demo** to test by yourself. For real Bluetooth messaging, allow Bluetooth access, open a real chat on the iPhone, and join from the Android app using the same pairing code.

Free-account signatures generally last **seven days**. Refresh/reinstall before they expire, especially before travelling. Sideloadly offers an automatic refresh feature, but verify the installation's validity before your trip. Free Apple accounts also limit the number of installed apps and registered app IDs. Authentication and installation remain subject to Apple's current service behaviour and the sideloading tool's compatibility.

## What is and is not tested

The Android APK, encryption/session tests, and browser demo have been checked. Unless the GitHub run has actually completed successfully, this document does not establish that the iOS app compiles. Actual iPhone-to-Samsung Bluetooth still needs testing on the two phones. The app does not require paid-only entitlements such as push notifications or app groups; its Bluetooth role is included in the native source.

## Official references

- GitHub standard runners and public-repository pricing: https://docs.github.com/en/actions/reference/runners/github-hosted-runners
- Sideloadly's free-account limits and Windows prerequisites: https://sideloadly.io/faq.html
- Apple's Personal Team provisioning limits: https://developer.apple.com/help/account/basics/about-your-developer-account
