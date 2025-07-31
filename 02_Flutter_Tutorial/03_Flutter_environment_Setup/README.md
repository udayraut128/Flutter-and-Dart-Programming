
# 🚀 3. Setting Up Flutter Environment

Setting up Flutter is your first step toward building cross-platform mobile apps. Here's a complete step-by-step guide:

---

## ✅ **1. Installing Flutter SDK**

### 🔧 Requirements:

* **OS**: Windows / macOS / Linux
* **Disk space**: \~2.8 GB (plus dependencies)
* **Tools**: Git, PowerShell (Windows), Terminal (macOS/Linux)

### 💻 Steps:

#### 🪟 **Windows**

1. **Download Flutter SDK**:
   👉 From [https://flutter.dev/docs/get-started/install](https://flutter.dev/docs/get-started/install)
2. Extract the zip file to `C:\src\flutter`
3. Add `C:\src\flutter\bin` to **Environment Variables > Path**
4. Run:

   ```bash
   flutter doctor
   ```

#### 🍎 **macOS**

1. Install Git:

   ```bash
   brew install git
   ```
2. Clone SDK:

   ```bash
   git clone https://github.com/flutter/flutter.git -b stable
   ```
3. Add Flutter to path:

   ```bash
   export PATH="$PATH:`pwd`/flutter/bin"
   ```
4. Run:

   ```bash
   flutter doctor
   ```

#### 🐧 **Linux**

1. Download SDK and extract:

   ```bash
   tar xf flutter_linux_<version>.tar.xz
   ```
2. Add `flutter/bin` to PATH
3. Run:

   ```bash
   flutter doctor
   ```

---

## ✅ **2. Setting up Android Studio / VS Code**

### 🧱 **Install Android Studio**

1. Download from: [https://developer.android.com/studio](https://developer.android.com/studio)
2. During setup, ensure the following plugins are selected:

   * **Android SDK**
   * **Android SDK Platform-Tools**
   * **Android Emulator**
3. After installation:

   * Go to **Settings > Plugins > Marketplace**
   * Search for **Flutter** → install → restart IDE
   * Dart plugin will install automatically

### 💡 Configure SDK location:

* Android Studio > Preferences > Appearance & Behavior > System Settings > Android SDK

---

### 🧑‍💻 **Install VS Code (Optional)**

1. Download from: [https://code.visualstudio.com](https://code.visualstudio.com)
2. Install **Flutter** & **Dart** extensions from Extensions panel
3. Install additional plugins: **Flutter Snippets**, **Awesome Flutter Snippets**

---

## ✅ **3. Emulator and Device Setup**

### 📱 Android Emulator

1. Open Android Studio → Tools → **Device Manager**
2. Click **Create Device**
3. Choose Pixel or Nexus → Click Next
4. Download any system image (e.g., API 33) → Finish

### Run emulator:

* From Device Manager → click ▶️ (Launch)
* OR in terminal:

  ```bash
  emulator -avd <emulator_name>
  ```

### 🔌 Real Device (Android)

1. Enable **Developer Options** → **USB Debugging**
2. Connect via USB
3. Run:

   ```bash
   flutter devices
   ```

---

## ✅ **4. Creating First App**

### Step-by-step:

```bash
flutter create my_first_app
cd my_first_app
flutter run
```

#### Folder structure:

```
my_first_app/
├── android/
├── ios/
├── lib/
│   └── main.dart   <-- Start coding here
├── test/
├── pubspec.yaml    <-- Dependencies & assets
```

### Example: Basic Flutter App

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My First App',
      home: Scaffold(
        appBar: AppBar(title: Text('Hello Flutter')),
        body: Center(child: Text('Welcome to Flutter!')),
      ),
    );
  }
}
```

Run using:

```bash
flutter run
```

---

## ✅ **flutter doctor**

This command checks if everything is installed correctly:

```bash
flutter doctor
```

Typical output:

```
[✓] Flutter (Channel stable, 3.x.x)
[✓] Android toolchain - develop for Android devices
[✓] Android Studio
[✓] VS Code
[✓] Connected device
```

If anything is ❌, it will guide you to fix it.

---
