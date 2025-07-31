### 🟢 **Topic 4: Variables in Dart**

A **variable** in Dart is a named storage that holds a value. Variables can be declared in several ways depending on mutability and typing needs.

---

### ✅ 1. **Declaring Variables**

You can declare variables using:

* Explicit type
* `var` (type inferred)
* `dynamic` (can change type at runtime)

```dart
int age = 25;
var name = 'Uday';       // inferred as String
dynamic anything = 100;  // can change type later
```

---

### ✅ 2. **Final and Const**

Both `final` and `const` are used for variables that **don't change**, but there's a key difference:

| Feature        | `final`                   | `const`               |
| -------------- | ------------------------- | --------------------- |
| Value assigned | At runtime                | At compile-time       |
| Reassignable   | No                        | No                    |
| Example        | `final name = getName();` | `const pi = 3.14159;` |

```dart
final date = DateTime.now(); // runtime
const year = 2025;           // compile-time
```

---

### ✅ 3. **Static Variables**

Used within classes to share a variable **across all instances**.

```dart
class Student {
  static int totalStudents = 0;
}
```

* Access: `Student.totalStudents`

---

### ✅ 4. **Late Variables**

Use `late` to **declare a variable without initializing** it immediately but ensure it **will be initialized before use**.

```dart
late String description;

void main() {
  description = "Dart variable example";
  print(description);
}
```

Useful with:

* `final` variables that get values later
* Expensive initializations

---

### ✅ 5. **Type Inference**

Dart can automatically infer the type from the assigned value.

```dart
var city = "Delhi";   // inferred as String
var age = 22;         // inferred as int
```

* If the value is changed to a **different type**, Dart throws an error (unless using `dynamic`).

---

### ✅ 6. **Variable Scope**

* **Local**: Inside functions or blocks.
* **Global**: Declared outside functions.
* **Instance**: Belongs to a class object.
* **Static**: Belongs to the class itself.

```dart
String global = "I'm global";

void show() {
  String local = "I'm local";
}
```

---

### ✅ Summary Table

| Keyword | Mutable | Type Safe | Compile-time | Scope       |
| ------- | ------- | --------- | ------------ | ----------- |
| var     | Yes     | Yes       | No           | Block       |
| final   | No      | Yes       | No           | Block/Class |
| const   | No      | Yes       | Yes          | Block/Class |
| dynamic | Yes     | No        | No           | Block       |
| late    | Yes     | Yes       | No           | Block/Class |

---

 