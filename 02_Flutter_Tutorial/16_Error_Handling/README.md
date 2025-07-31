## 🧩 1. `try-catch` in Dart/Flutter

### ✅ Purpose:

Used to **catch and handle exceptions** that might occur during runtime (e.g., file not found, network failure).

---

### 🔸 Syntax:

```dart
try {
  // Code that might throw an exception
} catch (e) {
  // Handle exception
}
```

---

### 🧪 Examples:

#### ✅ Example 1: Handling network failure

```dart
try {
  final response = await http.get(Uri.parse('https://invalid-url.com'));
  print(response.body);
} catch (e) {
  print('Network error: $e');
}
```

---

#### ✅ Example 2: Parsing invalid int

```dart
try {
  int value = int.parse("abc");
} catch (e) {
  print("Parsing error: $e");
}
```

---

#### ✅ Example 3: Multiple catch blocks with `on`

```dart
try {
  // Some risky code
} on FormatException catch (e) {
  print("Format Error: ${e.message}");
} catch (e) {
  print("General Error: $e");
}
```

---

## 🐞 2. `FlutterError`

### ✅ Purpose:

Flutter provides the `FlutterError` class to log framework-related issues, especially during **widget build or render phase**.

---

### 🔸 Usage:

```dart
FlutterError.onError = (FlutterErrorDetails details) {
  FlutterError.dumpErrorToConsole(details);
  // Custom action like reporting to a server
};
```

---

### 🧪 Examples:

#### ✅ Example 1: Customizing Flutter error behavior

```dart
void main() {
  FlutterError.onError = (FlutterErrorDetails details) {
    print("Caught Flutter error: ${details.exception}");
  };
  runApp(MyApp());
}
```

---

#### ✅ Example 2: Triggering a layout build error

```dart
Widget build(BuildContext context) {
  return Text(null); // Null causes exception in Text widget
}
```

> Will be reported via `FlutterError`.

---

#### ✅ Example 3: Logging widget tree issues

```dart
FlutterError.reportError(FlutterErrorDetails(
  exception: Exception('Custom widget error'),
  library: 'CustomLib',
  context: ErrorDescription('while building widget'),
));
```

---

## ⚠️ 3. `ErrorWidget`

### ✅ Purpose:

To **display a custom UI** instead of red error screen when a widget fails during build.

---

### 🔸 Usage:

```dart
ErrorWidget.builder = (FlutterErrorDetails details) {
  return Center(child: Text('Oops! Something went wrong.'));
};
```

---

### 🧪 Examples:

#### ✅ Example 1: Default ErrorWidget

Throws red error screen:

```dart
Text(null); // causes build failure
```

---

#### ✅ Example 2: Custom error widget

```dart
void main() {
  ErrorWidget.builder = (FlutterErrorDetails details) {
    return Center(child: Text('Something broke!'));
  };
  runApp(MyApp());
}
```

---

#### ✅ Example 3: Logging with error widget

```dart
ErrorWidget.builder = (details) {
  print("Widget Error: ${details.exception}");
  return Text('Error occurred!');
};
```

---

## 🧾 4. Logging Errors

### ✅ Purpose:

Capturing errors for debugging or reporting using tools like **`print()`**, **`logger` package**, or **remote monitoring**.

---

### 🧪 Examples:

#### ✅ Example 1: Basic logging

```dart
try {
  int x = int.parse('bad');
} catch (e, stack) {
  print("Error: $e\nStackTrace: $stack");
}
```

---

#### ✅ Example 2: Using `logger` package

```yaml
dependencies:
  logger: ^2.0.2
```

```dart
final log = Logger();

try {
  // Some error
} catch (e, stack) {
  log.e("Error occurred", e, stack);
}
```

---

#### ✅ Example 3: Sending to Firebase Crashlytics

```dart
FirebaseCrashlytics.instance.recordError(e, stack);
```

---

## 🌍 5. Global Error Handling

### ✅ Purpose:

Handle all **unhandled errors globally**, such as runtime errors or asynchronous exceptions.

---

### 🧪 Examples:

#### ✅ Example 1: Using `FlutterError.onError` (for UI errors)

```dart
FlutterError.onError = (FlutterErrorDetails details) {
  FlutterError.dumpErrorToConsole(details);
  // Send to analytics or logging
};
```

---

#### ✅ Example 2: Handling async errors (zones)

```dart
void main() {
  runZonedGuarded(() {
    runApp(MyApp());
  }, (error, stackTrace) {
    print("Caught async error: $error");
  });
}
```

---

#### ✅ Example 3: Crashlytics integration

```dart
FlutterError.onError = FirebaseCrashlytics.instance.recordFlutterFatalError;
```

---

### ✅ Example 4: Custom error screen globally

```dart
ErrorWidget.builder = (FlutterErrorDetails details) {
  return Scaffold(
    body: Center(child: Text("App Error!")),
  );
};
```

---

## 📌 Summary Table

| Concept         | Purpose                        | Example Usage                          |
| --------------- | ------------------------------ | -------------------------------------- |
| `try-catch`     | Catch runtime exceptions       | `try { risky code } catch (e) {}`      |
| `FlutterError`  | Handle widget framework errors | `FlutterError.onError = ...`           |
| `ErrorWidget`   | Customize widget error UI      | `ErrorWidget.builder = ...`            |
| Logging Errors  | Print/log error info           | `print()`, `logger.e()`, `Crashlytics` |
| Global Handling | Catch all uncaught exceptions  | `runZonedGuarded()`, `onError`         |

---
