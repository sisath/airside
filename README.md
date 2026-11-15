# Airside

An offline Bluetooth text messenger for an iPhone and Android phone.

The complete editable source, including Swift/Kotlin Bluetooth code, React Native screens, tests, and the dependency lockfile, is in **Airside-source.zip**. Extract it to work on the application. The cloud workflow unpacks the same archive before compiling it.

## Free iPhone build

Open **Actions > Build iPhone app (free sideload) > Run workflow**. After a successful run, download the **Airside-iPhone-unsigned** artifact and extract the IPA. Follow [FREE-IPHONE-INSTALL.md](FREE-IPHONE-INSTALL.md) to sign and install it from Windows using a free Apple account.

No Apple credentials are needed in GitHub. This repository uses a standard macOS runner for a public-repository build. The IPA is unsigned until a local sideloading tool signs it; it cannot be installed directly from Safari.

This is a personal-test application. The two-phone Bluetooth connection still needs checking on actual hardware before a flight. The app includes a clearly labelled solo demo.
