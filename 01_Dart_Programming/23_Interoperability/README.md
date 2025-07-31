# 🔷 23. Interoperability in Flutter

**Interoperability** means enabling communication between **Dart (Flutter)** and **native platform code** — like Java/Kotlin (Android) and Objective-C/Swift (iOS).

This is essential when:

* Flutter doesn't provide a direct plugin.
* You need low-level platform features (like Bluetooth, battery info, sensors, etc).

---

## 🔶 1. Calling Native Code in Flutter

To call **native Android/iOS APIs**, Flutter uses **Platform Channels**.

---

## 🔶 2. What are Platform Channels?

> A **Platform Channel** is a mechanism for **sending messages between Dart and the platform-specific code** (Java/Kotlin/Swift/Obj-C).

There are 3 types:

| Channel Type          | Direction     | Used For                                       |
| --------------------- | ------------- | ---------------------------------------------- |
| `MethodChannel`       | Dart ↔ Native | Calling platform methods (e.g., battery level) |
| `EventChannel`        | Native → Dart | Streams like sensors or location               |
| `BasicMessageChannel` | Dart ↔ Native | Raw binary/text message passing                |

---

## ✅ Example 1: Get Battery Level (using `MethodChannel`)

### 🔸 Dart (Flutter)

```dart
import 'package:flutter/services.dart';

class BatteryService {
  static const platform = MethodChannel('com.udayraut/battery');

  Future<String> getBatteryLevel() async {
    try {
      final int result = await platform.invokeMethod('getBatteryLevel');
      return 'Battery level: $result%';
    } catch (e) {
      return 'Failed to get battery level: $e';
    }
  }
}
```

### 🔸 Android Native Code (Kotlin)

`MainActivity.kt`

```kotlin
import android.os.BatteryManager
import android.os.Build
import android.os.Bundle
import io.flutter.embedding.android.FlutterActivity
import io.flutter.embedding.engine.FlutterEngine
import io.flutter.plugin.common.MethodChannel

class MainActivity: FlutterActivity() {
    private val CHANNEL = "com.udayraut/battery"

    override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
        super.configureFlutterEngine(flutterEngine)

        MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL).setMethodCallHandler {
            call, result ->
            if (call.method == "getBatteryLevel") {
                val batteryLevel = getBatteryLevel()

                if (batteryLevel != -1) {
                    result.success(batteryLevel)
                } else {
                    result.error("UNAVAILABLE", "Battery level not available.", null)
                }
            } else {
                result.notImplemented()
            }
        }
    }

    private fun getBatteryLevel(): Int {
        val batteryManager = getSystemService(BATTERY_SERVICE) as BatteryManager
        return batteryManager.getIntProperty(BatteryManager.BATTERY_PROPERTY_CAPACITY)
    }
}
```

---

## ✅ Example 2: Show Native Toast (Android)

### 🔸 Dart

```dart
static const platform = MethodChannel('com.udayraut/toast');

void showToast(String message) async {
  await platform.invokeMethod('showToast', {"message": message});
}
```

### 🔸 Kotlin

```kotlin
if (call.method == "showToast") {
    val msg = call.argument<String>("message")
    Toast.makeText(context, msg, Toast.LENGTH_SHORT).show()
    result.success(null)
}
```

---

## ✅ Example 3: Get Platform Version

### 🔸 Dart

```dart
static const platform = MethodChannel('samples.flutter.dev/info');

Future<String> getPlatformVersion() async {
  final version = await platform.invokeMethod('getPlatformVersion');
  return version;
}
```

### 🔸 Kotlin

```kotlin
if (call.method == "getPlatformVersion") {
    result.success("Android " + android.os.Build.VERSION.RELEASE)
}
```

---

## ✅ Example 4: Access Native Camera (via native integration)

Use `MethodChannel` to open the native camera and return the captured image path back to Flutter.

---

## 🔷 3. Summary Table

| Feature               | Description                                 | Example                     |
| --------------------- | ------------------------------------------- | --------------------------- |
| `MethodChannel`       | Call platform-specific code (one-time call) | Battery, Camera             |
| `EventChannel`        | Stream from platform to Flutter             | Sensors, GPS, Accelerometer |
| `BasicMessageChannel` | Bi-directional communication                | Send text or binary data    |

---

## 🧠 Best Practices

* Always wrap native calls in `try-catch` to handle exceptions.
* Use meaningful channel names like `"com.company/module"`.
* Consider writing a plugin if the logic is reusable across projects.

---

 