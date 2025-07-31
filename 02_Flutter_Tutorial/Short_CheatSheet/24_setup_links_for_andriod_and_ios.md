Setting up **App Links for Android** and **Universal Links for iOS** allows your app to **open automatically** when users click on a specific URL (like `https://example.com/profile/123`) instead of opening the browser. These are secure deep links that verify ownership of your domain.

---

## 📱 1. App Links (Android)

### ✅ Overview:

App Links are **HTTP(S)** URLs that open directly in your Android app, **if installed**. They are verified by Android using a **Digital Asset Links JSON file** hosted on your domain.

---

### 🧩 Steps to Set Up App Links in Flutter (Android)

### 1️⃣ Add Intent Filter in `AndroidManifest.xml`

Edit:

```xml
android/app/src/main/AndroidManifest.xml
```

Inside the `<activity>` tag:

```xml
<intent-filter android:autoVerify="true">
    <action android:name="android.intent.action.VIEW" />

    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />

    <!-- Example App Link -->
    <data
        android:scheme="https"
        android:host="example.com"
        android:pathPrefix="/profile" />
</intent-filter>
```

---

### 2️⃣ Host `assetlinks.json` on Your Website

Create a file:

```json
[
  {
    "relation": ["delegate_permission/common.handle_all_urls"],
    "target": {
      "namespace": "android_app",
      "package_name": "com.example.yourapp",
      "sha256_cert_fingerprints": [
        "A1:B2:C3:...:FF"  // ← Your release keystore fingerprint
      ]
    }
  }
]
```

✅ Host this file at:

```
https://example.com/.well-known/assetlinks.json
```

📌 You can test it using:

```bash
curl https://example.com/.well-known/assetlinks.json
```

---

### 3️⃣ Get SHA-256 Fingerprint

Use this command:

```bash
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
```

Look for `SHA-256:` value.

---

### 4️⃣ Handle the Link in Your Flutter Code

Use `uni_links` or `go_router` to capture the incoming URL:

```dart
import 'package:uni_links/uni_links.dart';

void initUniLinks() {
  uriLinkStream.listen((Uri? uri) {
    if (uri != null && uri.pathSegments.contains('profile')) {
      Navigator.pushNamed(context, '/profile/${uri.pathSegments.last}');
    }
  });
}
```

---

## 🍎 2. Universal Links (iOS)

### ✅ Overview:

Universal Links are Apple's secure way to open your app when a user taps a link to your website (`https://example.com/...`).

---

### 🧩 Steps to Set Up Universal Links in Flutter (iOS)

### 1️⃣ Add Associated Domains in Xcode

Open `ios/Runner.xcworkspace` in **Xcode**.

* Go to **Signing & Capabilities** tab.
* Click `+ Capability` → Add **Associated Domains**
* Add:

```
applinks:example.com
```

✅ This must match your domain exactly.

---

### 2️⃣ Host `apple-app-site-association` file

Host this file **without file extension** at:

```
https://example.com/.well-known/apple-app-site-association
```

> **Content-Type:** `application/json` (no `.json` extension)

```json
{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appID": "TEAMID.com.example.yourapp",
        "paths": [ "/profile/*", "/post/*" ]
      }
    ]
  }
}
```

* Replace `TEAMID` with your **Apple Developer Team ID**.
* Replace `com.example.yourapp` with your **iOS bundle ID**.

---

### 3️⃣ Handle Link in Flutter

Use `uni_links` package:

```dart
void handleLinks() async {
  final initialUri = await getInitialUri(); // for app launch
  uriLinkStream.listen((uri) {
    if (uri?.path == '/profile/123') {
      Navigator.pushNamed(context, '/profile/123');
    }
  });
}
```

---

### 4️⃣ Test Universal Links

#### ✅ Use iOS device (not simulator)

1. Send yourself a link (like via email)
2. Tap it on your iOS device
3. Your app should open directly to the corresponding page

---

## ✅ Summary Table

| Feature             | Android (App Links)                                  | iOS (Universal Links)                                           |
| ------------------- | ---------------------------------------------------- | --------------------------------------------------------------- |
| Required file       | `assetlinks.json`                                    | `apple-app-site-association`                                    |
| Hosted at           | `https://yourdomain.com/.well-known/assetlinks.json` | `https://yourdomain.com/.well-known/apple-app-site-association` |
| Android setup       | `AndroidManifest.xml` intent filter                  | Xcode: Associated Domains                                       |
| App opens for links | `https://yourdomain.com/...`                         | `https://yourdomain.com/...`                                    |
| Used for            | Secure deep links                                    | Secure deep links                                               |
| Flutter package     | `uni_links` or `go_router`                           | `uni_links` or `go_router`                                      |

---
 
