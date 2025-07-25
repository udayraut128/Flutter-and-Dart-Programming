### 🔗 Deep Linking in Flutter – Full Detailed Guide

**Deep linking** allows users to navigate directly to specific content or functionality within your app via a URL. For example, clicking on a link like `myapp://profile/123` should open the app and go directly to a user profile page.

---

## 🧭 Types of Deep Linking

| Type                      | Description                                                 |
| ------------------------- | ----------------------------------------------------------- |
| **Basic Deep Linking**    | Handles URLs when the app is already installed              |
| **Deferred Deep Linking** | Handles links even if the app wasn't installed yet          |
| **Universal/App Links**   | Secure deep links that open your app instead of the browser |

---

## 📦 Flutter Packages for Deep Linking

The most common package used for deep linking in Flutter is:

```yaml
uni_links: ^latest_version
```

> Also consider:
>
> * `go_router` (for declarative navigation + deep links)
> * `firebase_dynamic_links` (for deferred links via Firebase)

---

## 🧱 Step-by-Step Setup with `uni_links` (For Android and iOS)

### 1️⃣ Add the Package

```yaml
dependencies:
  uni_links: ^latest_version
```

Run:

```bash
flutter pub get
```

---

### 2️⃣ Configure Platform-Specific Settings

#### 🔧 Android (AndroidManifest.xml)

Edit `android/app/src/main/AndroidManifest.xml`:

```xml
<activity
  android:name=".MainActivity"
  android:launchMode="singleTask"
  android:exported="true"
  android:theme="@style/LaunchTheme"
  android:configChanges="keyboard|keyboardHidden|orientation|screenSize|locale|layoutDirection|fontScale|screenLayout|density|uiMode"
  android:hardwareAccelerated="true"
  android:windowSoftInputMode="adjustResize">
  
  <intent-filter>
    <action android:name="android.intent.action.VIEW"/>
    <category android:name="android.intent.category.DEFAULT"/>
    <category android:name="android.intent.category.BROWSABLE"/>

    <!-- Your app’s scheme and host -->
    <data android:scheme="myapp" android:host="profile"/>
  </intent-filter>

</activity>
```

Now `myapp://profile/123` will be handled by your app.

---

#### 🍏 iOS (Info.plist)

Edit `ios/Runner/Info.plist`:

```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>myapp</string>
    </array>
  </dict>
</array>
```

---

### 3️⃣ Handle Deep Links in Flutter Code

#### 🌐 Import the package

```dart
import 'package:uni_links/uni_links.dart';
import 'dart:async';
```

#### 🔍 Listen for incoming links

```dart
StreamSubscription? _sub;

@override
void initState() {
  super.initState();
  _handleIncomingLinks();
}

void _handleIncomingLinks() {
  _sub = uriLinkStream.listen((Uri? uri) {
    if (uri != null) {
      print("Incoming URI: $uri");
      // Example: Navigate based on path or query
      if (uri.pathSegments.contains('profile')) {
        final userId = uri.pathSegments.last;
        Navigator.pushNamed(context, '/profile/$userId');
      }
    }
  }, onError: (err) {
    print("Failed to receive link: $err");
  });
}

@override
void dispose() {
  _sub?.cancel();
  super.dispose();
}
```

---

### 4️⃣ Test Deep Links

#### 🧪 On Android:

Use adb:

```bash
adb shell am start -a android.intent.action.VIEW \
    -d "myapp://profile/123" \
    your.package.name
```

#### 🧪 On iOS:

Use Safari on simulator:

```text
myapp://profile/123
```

---

## 🚀 Navigation with `go_router` (Alternative)

If you're using `go_router`, it handles deep links automatically via routes and parameters.

```dart
final _router = GoRouter(
  routes: [
    GoRoute(
      path: '/profile/:id',
      builder: (context, state) {
        final id = state.params['id']!;
        return ProfileScreen(userId: id);
      },
    ),
  ],
);
```

Now `myapp://profile/123` opens `ProfileScreen` with `userId = 123`.

---

## 🔒 Universal Links and App Links (Advanced)

For real-world apps:

* Use [App Links](https://developer.android.com/training/app-links) (Android)
* Use [Universal Links](https://developer.apple.com/ios/universal-links/) (iOS)
* Requires domain ownership and file hosting (like `apple-app-site-association` file)

---

## 📄 Summary

| Task                  | Done with                                         |
| --------------------- | ------------------------------------------------- |
| Configure Android/iOS | AndroidManifest.xml / Info.plist                  |
| Add package           | `uni_links` or `go_router`                        |
| Handle navigation     | Based on URI path/query                           |
| Test on devices       | `adb` / Safari / QR links                         |
| For advanced linking  | Use Firebase Dynamic Links or App/Universal Links |

---

 