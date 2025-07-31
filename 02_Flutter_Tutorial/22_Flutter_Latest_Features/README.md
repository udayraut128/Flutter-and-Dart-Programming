## 🔹 1. Material 3 Support in Flutter

### 🔸 What is Material 3?

Material 3 (also known as Material You) is Google’s latest design system that supports:

* Dynamic color theming
* Updated components
* Better accessibility
* Rounded corners, large typography, adaptive design

Flutter officially supports **Material 3** starting from version `3.0.0` and above.

---

### ✅ Key Features of Material 3 in Flutter:

* `useMaterial3: true` in `ThemeData`
* New widgets: `FilledButton`, `IconButton.filledTonal`, `NavigationBar` (replacing BottomNavigationBar), `SegmentedButton`, etc.
* Dynamic color from device (Android 12+)

---

### 📌 Example 1: Enabling Material 3

```dart
MaterialApp(
  theme: ThemeData(
    colorSchemeSeed: Colors.teal,
    useMaterial3: true,
  ),
  home: HomePage(),
);
```

This enables Material 3 styling across all supported widgets.

---

### 📌 Example 2: Using Material 3 Buttons

```dart
Column(
  children: [
    FilledButton(
      onPressed: () {},
      child: Text('Filled Button'),
    ),
    OutlinedButton(
      onPressed: () {},
      child: Text('Outlined Button'),
    ),
    TextButton(
      onPressed: () {},
      child: Text('Text Button'),
    ),
  ],
)
```

These buttons have updated padding, elevation, and corner radius as per Material 3 specs.

---

### 📌 Example 3: NavigationBar (Material 3)

```dart
NavigationBar(
  selectedIndex: 0,
  destinations: const [
    NavigationDestination(
      icon: Icon(Icons.home),
      label: 'Home',
    ),
    NavigationDestination(
      icon: Icon(Icons.settings),
      label: 'Settings',
    ),
  ],
)
```

This replaces the traditional `BottomNavigationBar` with a more modern Material 3 UI.

---

## 🔹 2. Null Safety Enhancements

### 🔸 What is Null Safety?

Introduced in Dart 2.12+, null safety ensures that variables **can't be null unless explicitly allowed**. This prevents runtime null exceptions and improves app stability.

---

### ✅ Key Concepts:

* `String name;` → must be initialized
* `String? name;` → nullable
* `late String name;` → promises to initialize before use

---

### 📌 Example 1: Declaring Nullable vs Non-nullable

```dart
String name = 'Uday';       // Cannot be null
String? nickname;           // Can be null
```

---

### 📌 Example 2: Null-aware operators

```dart
String? name;
print(name ?? 'Guest');      // Output: Guest
```

Other operators:

* `??=` assigns default if null
* `!` asserts value is not null

---

### 📌 Example 3: Late Initialization

```dart
late String description;

void main() {
  description = 'This is late initialized';
  print(description);
}
```

Use `late` when you’re sure a variable will be initialized before use.

---

### ✅ Null Safety Benefits:

* Compile-time errors instead of runtime crashes
* Better performance (no null checks at runtime)
* Safer APIs for developers

---

## 🔷 1. **New Lifecycle APIs in Flutter**

### 🔹 What is it?

Flutter’s **new lifecycle APIs** give developers better control and insight into a widget’s lifecycle, especially useful when handling app visibility, background/foreground transitions, or conserving resources like camera/audio when the app is not in focus.

> These APIs are part of the \[WidgetsBindingObserver] or `AppLifecycleListener` class (newer & cleaner), introduced in newer versions of Flutter.

---

### ✅ Key Lifecycle States:

* `AppLifecycleState.resumed`: App is in foreground and interactive
* `AppLifecycleState.inactive`: App is inactive (e.g. incoming call, control center)
* `AppLifecycleState.paused`: App is not visible (background)
* `AppLifecycleState.detached`: App is still hosted but detached from view

---

### 📌 Example 1: Using AppLifecycleListener (Newer API)

```dart
class MyHomePage extends StatelessWidget {
  MyHomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return AppLifecycleListener(
      onStateChange: (state) {
        if (state == AppLifecycleState.paused) {
          print("App in background");
        } else if (state == AppLifecycleState.resumed) {
          print("App resumed");
        }
      },
      child: Scaffold(
        appBar: AppBar(title: Text("Lifecycle Example")),
        body: Center(child: Text("Observe lifecycle changes")),
      ),
    );
  }
}
```

---

### 📌 Example 2: Using `WidgetsBindingObserver` (Traditional API)

```dart
class MyHomePage extends StatefulWidget {
  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> with WidgetsBindingObserver {
  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void didChangeAppLifecycleState(AppLifecycleState state) {
    print("Lifecycle changed: $state");
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(body: Center(child: Text("Lifecycle Monitor")));
  }
}
```

---

### 📌 Example 3: Use Case - Pause a Video Player

```dart
onStateChange: (state) {
  if (state == AppLifecycleState.paused) {
    _videoController.pause();
  }
}
```

---

## 🔷 2. **Impeller Renderer (Performance Boost)**

### 🔹 What is Impeller?

**Impeller** is Flutter’s new rendering engine (replacing Skia on some platforms). It’s **precompiled**, eliminating shader compilation jank, which leads to:

* Smoother animations
* No shader warm-up jank
* Better performance on iOS (default) and Android (optional)

> As of Flutter 3.10+, Impeller is **default for iOS** and **experimental for Android**.

---

### ✅ Why Use Impeller?

* Uses Metal (iOS) and Vulkan (Android)
* Pre-compiles shaders at build time
* Removes runtime shader compilation delays

---

### 📌 Example 1: Enable Impeller on Android (if using Flutter 3.13+)

Add to `android/gradle.properties`:

```properties
flutter.renderer=impeller
```

Or launch via:

```bash
flutter run --enable-impeller
```

---

### 📌 Example 2: Impeller Default on iOS

No action needed from Flutter 3.10+ onward. You’ll notice smoother transitions especially on animation-heavy UIs.

---

### 📌 Example 3: App With Complex Animation

Without Impeller:

* Initial animations may **stutter** on first load (due to runtime shader compilation)

With Impeller:

* Animations are **smooth and consistent** right from app start

---

### 🔎 How to Check If Impeller Is Active

Run the app and check logs:

```bash
flutter run -v
```

You’ll see:

```
Impeller enabled: true
```

---

### 🔧 When Should You Use Impeller?

* Always use it on iOS (default)
* Test it on Android with `--enable-impeller` (still improving support)
* Especially great for apps with:

  * Heavy animations
  * Custom painting
  * Lots of transitions and UI shaders

---
