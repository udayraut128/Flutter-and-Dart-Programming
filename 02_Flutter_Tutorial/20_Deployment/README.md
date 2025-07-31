## 🚀 Deployment in Flutter

Flutter allows you to build apps for multiple platforms from a **single codebase**. Deployment is the final phase where you build, sign, and publish your app to stores or devices.

---

## ✅ 1. Building APK / IPA (Android & iOS Builds)

### 📌 Android (APK / AAB)

#### 📦 Building a Debug APK:

```bash
flutter build apk
```

#### 📦 Building a Release APK:

```bash
flutter build apk --release
```

#### 📦 Building Android App Bundle (AAB):

```bash
flutter build appbundle --release
```

**Use AAB for Play Store.**

---

### 🔍 Example 1:

```bash
flutter build apk --split-per-abi
```

➡️ Creates APKs for different CPU architectures (`armeabi`, `x86_64`).

---

### 🔍 Example 2:

```bash
flutter build apk --flavor prod -t lib/main_prod.dart
```

➡️ Build a flavor-specific APK (e.g., for production).

---

### 📌 iOS (IPA)

You **must use a macOS system** with Xcode.

#### 📦 Building iOS release:

```bash
flutter build ios --release
```

Open in Xcode:

```bash
open ios/Runner.xcworkspace
```

Then archive and upload via **Xcode Organizer**.

---

### 🔍 Example 3:

```bash
flutter build ios --release --no-codesign
```

➡️ Build IPA without code signing (useful for testing).

---

### 🔍 Example 4:

Using Fastlane for iOS & Android automation:

```bash
fastlane beta
```

---

## ✅ 2. Signing Apps (Android & iOS)

### 📌 Android App Signing

1. Generate keystore:

```bash
keytool -genkey -v -keystore my-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-key
```

2. Configure in `android/key.properties`:

```properties
storePassword=your_store_pass
keyPassword=your_key_pass
keyAlias=my-key
storeFile=../my-key.jks
```

3. Link in `android/app/build.gradle`:

```gradle
signingConfigs {
    release {
        storeFile file(keyProperties['storeFile'])
        storePassword keyProperties['storePassword']
        keyAlias keyProperties['keyAlias']
        keyPassword keyProperties['keyPassword']
    }
}
```

---

### 📌 iOS App Signing

Use **Xcode** to:

* Select provisioning profile
* Use automatic signing or manual team ID
* Archive and upload to App Store

---

### 🔍 Example 1:

Manual signing:

* Open Xcode → Select Target → Signing & Capabilities → Team → Select Apple ID

---

### 🔍 Example 2:

Use automatic code signing:

```bash
flutter build ios --release --codesign
```

---

### 🔍 Example 3:

CI/CD sign with environment variables:

```yaml
storePassword: ${{ secrets.STORE_PASSWORD }}
```

---

## ✅ 3. Play Store & App Store Deployment

### 📌 Play Store (Android)

1. Build `.aab`:

```bash
flutter build appbundle
```

2. Go to [Google Play Console](https://play.google.com/console)
3. Create a new release → Upload `.aab` → Set app details → Submit for review

---

### 📌 App Store (iOS)

1. Archive in Xcode
2. Use **App Store Connect** to submit
3. Follow the review process

---

### 🔍 Example 1:

Include **Screenshots**, **Privacy Policy**, and **App Icon (512x512)** for Play Store.

---

### 🔍 Example 2:

Use `fastlane`:

```bash
fastlane supply --aab app-release.aab
```

---

### 🔍 Example 3:

iOS Transporter app to upload `.ipa`:

* Open Transporter
* Sign in with Apple ID
* Upload `.ipa` from `build/ios/ipa`

---

### 🔍 Example 4:

Use CI/CD (e.g., GitHub Actions) to automate upload.

---

## ✅ 4. Web Deployment

### 📌 Flutter Web Support:

Run:

```bash
flutter build web
```

Output in:

```
/build/web/
```

You can host it on:

* GitHub Pages
* Firebase Hosting
* Netlify / Vercel

---

### 🔍 Example 1: GitHub Pages

```bash
flutter build web
```

Then push `/build/web` to the `gh-pages` branch.

---

### 🔍 Example 2: Firebase Hosting

```bash
firebase init hosting
flutter build web
firebase deploy
```

---

### 🔍 Example 3: Netlify

* Drag and drop `build/web` folder to Netlify UI or use CLI.

---

### 🔍 Example 4:

Run locally for testing:

```bash
flutter run -d chrome
```

---

## ✅ 5. Desktop Deployment

Flutter supports Windows, macOS, and Linux (stable).

Enable it:

```bash
flutter config --enable-windows-desktop
flutter config --enable-macos-desktop
flutter config --enable-linux-desktop
```

Build:

```bash
flutter build windows
flutter build macos
flutter build linux
```

---

### 🔍 Example 1: Windows EXE

```bash
flutter build windows
```

➡️ Output: `build/windows/runner/Release/app.exe`

---

### 🔍 Example 2: macOS App

```bash
flutter build macos
```

➡️ Output: `.app` folder for macOS

---

### 🔍 Example 3: Linux App

```bash
flutter build linux
```

---

### 🔍 Example 4: Publish to Snap Store (Linux)

* Use `snapcraft.yaml`
* Publish via `snapcraft`

---

## ✅ Summary Table

| Platform    | Command                   | Output            | Notes                           |
| ----------- | ------------------------- | ----------------- | ------------------------------- |
| Android APK | `flutter build apk`       | `app-release.apk` | Use for direct install          |
| Android AAB | `flutter build appbundle` | `app-release.aab` | Use for Play Store              |
| iOS         | `flutter build ios`       | IPA via Xcode     | Needs macOS                     |
| Web         | `flutter build web`       | HTML, JS, CSS     | Host via Firebase, GitHub Pages |
| Windows     | `flutter build windows`   | `.exe` app        | Supported in stable             |
| macOS       | `flutter build macos`     | `.app`            | Needs macOS                     |
| Linux       | `flutter build linux`     | Executable binary | Requires GTK dependencies       |

---

