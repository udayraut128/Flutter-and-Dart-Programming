## ✅ 1. Platform Channels

### 📌 What is it?

Platform Channels allow **Flutter (Dart)** to communicate with **native platform code** (Java/Kotlin for Android, Objective-C/Swift for iOS).

---

### 🔧 How it works:

* Dart sends a message through a `MethodChannel`.
* Native code listens for that channel and executes platform-specific logic.
* Result is returned back to Flutter.

---

### 🔄 Example Use Case:

You want to get the **battery level** from native Android/iOS.

### Flutter Side (Dart):

```dart
static const platform = MethodChannel('samples.flutter.dev/battery');

Future<void> getBatteryLevel() async {
  try {
    final int result = await platform.invokeMethod('getBatteryLevel');
    print("Battery level is $result%");
  } catch (e) {
    print("Failed to get battery level: $e");
  }
}
```

### Android Side (Kotlin):

```kotlin
class MainActivity : FlutterActivity() {
  private val CHANNEL = "samples.flutter.dev/battery"

  override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
    super.configureFlutterEngine(flutterEngine)
    MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL).setMethodCallHandler {
      call, result ->
      if (call.method == "getBatteryLevel") {
        val batteryLevel = getBatteryLevel()
        result.success(batteryLevel)
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

### 🧪 More Examples:

1. Get device IMEI (Android)
2. Launch a native Android/iOS screen
3. Open app settings page using native code

---

## ✅ 2. Calling Native Code (Android/iOS)

### 📌 What is it?

Using Platform Channels, you can run **native SDK features** not available in Flutter directly.

---

### 🧪 Example 1: Native Toast in Android

```dart
MethodChannel('my.channel').invokeMethod('showToast');
```

**Kotlin:**

```kotlin
Toast.makeText(context, "Hello from native!", Toast.LENGTH_SHORT).show()
```

---

### 🧪 Example 2: Get Android Version

```dart
final result = await platform.invokeMethod('getAndroidVersion');
```

**Kotlin:**

```kotlin
call.method == "getAndroidVersion" -> result.success(Build.VERSION.RELEASE)
```

---

### 🧪 Example 3: Get iOS Device Info

**Swift:**

```swift
if call.method == "getDeviceName" {
    result(UIDevice.current.name)
}
```

---

### 🧪 Example 4: Open native camera

Use native intents on Android or UIImagePickerController on iOS.

---

## ✅ 3. Permissions (Using `permission_handler`)

### 📌 What is it?

The [`permission_handler`](https://pub.dev/packages/permission_handler) package helps you **request and check app permissions** at runtime.

---

### 🧪 Example 1: Request Camera Permission

```dart
PermissionStatus status = await Permission.camera.request();
if (status.isGranted) {
  print("Camera permission granted");
}
```

---

### 🧪 Example 2: Check location permission

```dart
if (await Permission.location.isGranted) {
  print("Location permission already granted");
}
```

---

### 🧪 Example 3: Open App Settings

```dart
openAppSettings();
```

---

### 🧪 Example 4: Request multiple permissions

```dart
Map<Permission, PermissionStatus> statuses = await [
  Permission.camera,
  Permission.microphone,
].request();
```

---

## ✅ 4. Battery, Sensors, Camera, GPS Access

---

### 🔋 Battery

#### Example 1: Using `battery_plus`

```yaml
battery_plus: ^5.0.0
```

```dart
final battery = Battery();
int level = await battery.batteryLevel;
print("Battery Level: $level%");
```

---

### 📱 Sensors (Accelerometer, Gyroscope)

#### Example 2: Using `sensors_plus`

```yaml
sensors_plus: ^4.0.2
```

```dart
accelerometerEvents.listen((AccelerometerEvent event) {
  print("X: ${event.x}, Y: ${event.y}, Z: ${event.z}");
});
```

---

### 📷 Camera

#### Example 3: Using `camera` package

```yaml
camera: ^0.10.5+3
```

```dart
final cameras = await availableCameras();
CameraController controller = CameraController(cameras[0], ResolutionPreset.high);
await controller.initialize();
```

---

### 📍 GPS (Location)

#### Example 4: Using `geolocator`

```yaml
geolocator: ^10.1.0
```

```dart
Position position = await Geolocator.getCurrentPosition(
    desiredAccuracy: LocationAccuracy.high);
print("Latitude: ${position.latitude}, Longitude: ${position.longitude}");
```

---

## ✅ Summary Table

| Feature               | Description                   | Example                               |
| --------------------- | ----------------------------- | ------------------------------------- |
| Platform Channels     | Communicate with native code  | Battery level, Toast                  |
| Calling Native Code   | Use Android/iOS SDK features  | Device Info, Camera Intent            |
| Permissions           | Request and check permissions | Camera, Microphone, Location          |
| Battery, Sensors, GPS | Access hardware features      | Battery %, Accelerometer, GPS, Camera |

---

