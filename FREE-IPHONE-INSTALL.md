# Install CloseBy on iPhone from Windows

The supplied GitHub workflow builds an unsigned physical-iPhone app on a standard macOS runner. The repository currently stores a source ZIP named Airside-source.zip for workflow compatibility; it contains the CloseBy project in an airside folder. The repository name and internal identifiers retain their original names.

1. Open the repository's Actions page and choose Build iPhone app (free sideload), then Run workflow on main.
2. Wait for the exact source revision's run to succeed. Download its Airside-iPhone-unsigned artifact. Extract the ZIP; the payload IPA is build/ios-unsigned/Airside-unsigned.ipa. The visible app name is CloseBy.
3. On Windows use Sideloadly from https://sideloadly.io/ and its documented desktop iTunes/iCloud prerequisites. The Apple Devices app can also help establish the iPhone's trusted connection. Use a working data cable directly to the PC; unlock the phone and complete Trust prompts.
4. Load the IPA and select the iPhone. Use the same Apple account and bundle identifier as the existing install to update it. Enter passwords and verification codes directly in Sideloadly yourself.
5. After Done / 100%, open CloseBy. Complete developer trust or Developer Mode prompts yourself if required, and allow Bluetooth.
6. A free Apple account normally signs an app for seven days; refresh it from the PC before expiry. Wi-Fi refresh requires an initial trusted USB setup and wireless-device visibility enabled. See https://sideloadly.io/faq.html for current requirements.

The group protocol requires the new CloseBy build on every participant's phone; old Airside builds cannot join. Choose Try the demo for a solo three-person simulation. For actual group radio behavior, follow INSTALL.md and test on physical phones.
