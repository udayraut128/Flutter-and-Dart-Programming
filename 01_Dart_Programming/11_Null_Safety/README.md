## 🟢 **Topic 11: Null Safety in Dart**

Null safety is one of Dart's most important features. It helps you avoid **null reference errors**, one of the most common bugs in programming.

---

### 🔸 What is Null?

In Dart, `null` means "no value" or "nothing".

Example:

```dart
String? name = null;
```

If you try to use a `null` value where a non-null is expected, you get a compile-time error (thanks to **null safety**).

---

### ✅ 1. **Nullable and Non-nullable Types**

* **Non-nullable**: Cannot be assigned `null`

  ```dart
  String name = 'Uday';  // Can't be null
  ```

* **Nullable**: Can be assigned `null`, use `?`

  ```dart
  String? nickname = null;
  ```

---

### ✅ 2. **Null-aware Operators**

| Operator | Description                         | Example          |
| -------- | ----------------------------------- | ---------------- |
| `?`      | Marks a type as nullable            | `int? a = null;` |
| `??`     | Default value if null               | `a = b ?? 0;`    |
| `?.`     | Access member only if not null      | `name?.length`   |
| `??=`    | Assign value only if currently null | `a ??= 10;`      |
| `!`      | Force non-null (use carefully!)     | `name!.length`   |

---

### 🔹 Example 1: Default Value with `??`

```dart
String? name;
print(name ?? "Guest"); // Output: Guest
```

---

### 🔹 Example 2: Safe Access with `?.`

```dart
String? username;
print(username?.toUpperCase()); // Output: null, no error
```

---

### 🔹 Example 3: Force Non-null with `!`

```dart
String? email = 'test@example.com';
print(email!.length);  // Works fine

String? e;
print(e!.length);  // ❌ Error at runtime (Null check operator used on null)
```

---

### ✅ 3. **Late Keyword with Null Safety**

You can use `late` to tell Dart: "I will assign this variable later before using it."

```dart
late String description;
description = "Dart is great!";
print(description); // ✅ Works
```

---

### ✅ 4. **Function Parameters with Null Safety**

You can make function parameters:

* **Optional and nullable**
* **Non-nullable with default values**

```dart
void greet(String name, [String? message]) {
  print('Hello $name. ${message ?? ""}');
}
```

---

### ✅ 5. **Nullable Return Types**

```dart
String? getName(bool show) {
  if (show) return "Uday";
  return null;
}
```

---

### 🧠 Why Is Null Safety Important?

It prevents this common error:

```dart
String name;
print(name.length); // ❌ Error: name is not initialized
```

With null safety:

* Compiler warns you
* Bugs are reduced
* Your code is safer and easier to maintain

---

### ✅ Summary Table

| Concept             | Code Example         |
| ------------------- | -------------------- |
| Nullable type       | `int? age = null;`   |
| Default value       | `var a = age ?? 18;` |
| Safe access         | `user?.email`        |
| Force non-null      | `email!`             |
| Late initialization | `late String id;`    |

---

