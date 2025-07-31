## 🟩 **Topic 22: Security and Best Practices in Dart**

Security and best practices in Dart (especially when using it with Flutter) help ensure your code is **safe, maintainable, and high-performing**. Dart is designed with **type safety** and **performance** in mind, but it’s still essential to follow guidelines that avoid vulnerabilities and inefficiencies.

---

### 🔹 22.1: **Type Safety**

Dart is a **soundly typed language** — meaning:

* You **can’t assign a value of one type to another incompatible type**.
* Helps catch bugs at compile-time instead of runtime.

#### ✅ Example

```dart
int count = 5;
// count = "hello"; // ❌ Compile-time error
```

🔐 **Benefits of type safety:**

* Prevents runtime type errors.
* Improves code readability.
* Easier debugging.

#### Use `late`, `final`, and `const` appropriately:

```dart
final name = "Uday"; // Can’t be reassigned
const pi = 3.14;     // Compile-time constant
late String userId;  // Initialized later before use
```

---

### 🔹 22.2: **Code Optimization**

#### ✅ Minimize unnecessary rebuilds (especially in Flutter):

* Use `const` widgets where possible.
* Avoid placing `setState()` too frequently.
* Prefer `ListView.builder` over `ListView(children: [...])` for large lists.

#### ✅ Example of const widget optimization:

```dart
const Text('Hello'); // Compile-time constant widget
```

---

### 🔹 22.3: **Defensive Programming**

Write code that can handle unexpected inputs or states.

#### ✅ Example:

```dart
String getName(String? name) {
  return name ?? 'Guest'; // Default to 'Guest' if null
}
```

#### Other defensive techniques:

* Use `assert()` during development.
* Validate user inputs and API responses.
* Handle all exceptions with `try-catch`.

---

### 🧠 Other Best Practices

| Area           | Good Practice                                    |
| -------------- | ------------------------------------------------ |
| 🚀 Performance | Use `const`, avoid large object recreation       |
| 🧪 Testing     | Write unit tests, mock dependencies              |
| 🧹 Clean Code  | Use meaningful names, avoid deeply nested code   |
| 🔁 Null Safety | Handle nullable variables properly               |
| 📦 Packages    | Use trusted packages (verify pub.dev publishers) |

---

### 🔐 Security-Specific Practices

* Don’t store secrets (API keys, tokens) in code. Use **.env** or **platform-specific secure storage**.
* Use `flutter_secure_storage` for sensitive data.
* Use HTTPS for all API communication.
* Validate all input from users or APIs.
* Avoid dynamic code execution like `eval()`.

---

### 🔧 Example: Secure Token Storage

```dart
import 'package:flutter_secure_storage/flutter_secure_storage.dart';

final storage = FlutterSecureStorage();

// Write
await storage.write(key: 'token', value: 'abc123');

// Read
String? token = await storage.read(key: 'token');
```

---

## ✅ Summary

* Dart is strongly and soundly typed — use it to your advantage.
* Optimize performance with `const`, lazy loading, and efficient lists.
* Defend against bad data using null checks, default values, and validations.
* Don’t expose sensitive data. Use secure storage.
* Follow clean code principles and test thoroughly.

---
 