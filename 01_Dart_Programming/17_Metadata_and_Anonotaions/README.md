## 🟪 **Topic 17: Metadata & Annotations in Dart**

---

### 📌 What is Metadata in Dart?

**Metadata** in Dart is extra information added to your code using **annotations** (prefixed with `@`).
These annotations **don’t affect** the runtime behavior directly but **inform the compiler**, **tools**, or **readers** about something special in the code.

---

### ✅ Why Use Annotations?

* Add **metadata** to classes, methods, or variables.
* Used by **tools**, **compilers**, or **frameworks** like Flutter.
* Improve **code clarity**, enable **linting**, or **custom behavior**.

---

## 🔹 17.1: Built-in Annotations

---

### 🔸 `@override`

Used to indicate that a method is **overriding** a method in its superclass.

```dart
class Animal {
  void speak() => print("Animal sound");
}

class Dog extends Animal {
  @override
  void speak() => print("Bark");
}

void main() {
  Dog().speak(); // Output: Bark
}
```

✅ Helps prevent typos and incorrect overrides.

---

### 🔸 `@deprecated`

Marks a piece of code as **deprecated** (discouraged from use).
It shows a **warning** during compilation.

```dart
@deprecated
void oldFunction() {
  print("This function is outdated.");
}

void main() {
  oldFunction(); // Warning: deprecated
}
```

---

### 🔸 `@pragma`

Used for **compiler-specific** instructions (mostly internal).
Example:

```dart
@pragma("vm:entry-point")
void entry() => print("Entry point for VM.");
```

---

## 🔹 17.2: Custom Annotations

You can define your **own metadata** using annotation classes.

---

### 🔸 Step 1: Create Annotation Class

```dart
class Developer {
  final String name;
  const Developer(this.name);
}
```

### 🔸 Step 2: Use the Annotation

```dart
@Developer('Uday Raut')
class MyApp {
  void run() => print("Running App...");
}
```

---

### 🔸 Important Notes:

* Custom annotations must be marked `const`.
* Can be applied to classes, methods, variables, etc.

---

## 🔹 17.3: Using Metadata with Reflection (Advanced)

You can use packages like `reflectable` to read annotations at runtime (not typically used in beginner apps or Flutter).

---

## ✅ Use Cases for Metadata in Dart & Flutter

| Annotation             | Purpose                           |
| ---------------------- | --------------------------------- |
| `@override`            | Ensures method properly overrides |
| `@deprecated`          | Marks code as outdated            |
| `@required` (Flutter)  | Marks parameter as required       |
| `@immutable` (Flutter) | Ensures object can’t be modified  |
| Custom Annotations     | Used for tooling or frameworks    |

---

## 🧠 Summary

* Annotations are metadata applied with `@`.
* Dart provides **built-in annotations** like `@override`, `@deprecated`, etc.
* You can create **custom annotations** using constant classes.

---
 