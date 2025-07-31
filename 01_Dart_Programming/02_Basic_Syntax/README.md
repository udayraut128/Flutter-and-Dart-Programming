### 🟢 **Topic 2: Basic Syntax in Dart**

Understanding the **basic syntax** is essential before diving deeper into Dart. Here's a breakdown:

---

#### 📌 1. **main() Function**

* This is the **entry point** of every Dart program.
* Execution starts from `main()`.

```dart
void main() {
  print('Hello, Dart!');
}
```

---

#### 📌 2. **Comments**

Used to explain code. Dart supports three types of comments:

* **Single-line comment:**

  ```dart
  // This is a single-line comment
  ```

* **Multi-line comment:**

  ```dart
  /* This is a 
     multi-line comment */
  ```

* **Documentation comment:**

  ```dart
  /// This describes a class or function
  ```

---

#### 📌 3. **Printing Output**

To display output in Dart, use `print()`:

```dart
print("Hello, World!");
```

Output:

```
Hello, World!
```

---

#### 📌 4. **Identifiers**

Identifiers are names for variables, functions, classes, etc.

**Rules:**

* Must begin with a letter (a–z, A–Z) or an underscore (\_).
* Can contain letters, digits (0–9), and underscores.
* Cannot be a **keyword** (like `class`, `void`, etc.)

```dart
int age = 20;      // valid
var _name = "Bob"; // valid
```

---

#### 📌 5. **Keywords**

Dart has **reserved words** that cannot be used as identifiers.

Examples:

```dart
abstract, class, const, continue, default, do, else,
enum, extends, false, final, for, if, implements,
import, in, interface, is, new, null, return, super, this, true, void, while
```

---

#### 📌 6. **Semicolons**

Dart statements must end with a **semicolon (`;`)**.

```dart
int x = 10;
print(x);
```

---

#### 📌 7. **Case Sensitivity**

Dart is **case-sensitive**, meaning `myVar`, `MyVar`, and `MYVAR` are different.

```dart
var a = 10;
var A = 20;
print(a); // 10
print(A); // 20
```

---

#### 📌 8. **Whitespace and Formatting**

* Dart **ignores extra whitespace** and line breaks.
* Use whitespace for **readability**.

```dart
int a = 5;
int b = 6;
int sum = a + b;
print(sum); // 11
```

---

#### 📌 9. **Statements and Expressions**

* A **statement** performs an action.
* An **expression** evaluates to a value.

```dart
var x = 10 + 5;  // expression
print(x);        // statement
```

---

#### 📌 10. **Dart Style Guide**

* Use camelCase for variables and functions: `myVariable`, `getUser()`
* Use PascalCase for class names: `StudentProfile`

---

 