### 🟢 **Topic 3: Data Types in Dart**

Dart is a **strongly typed language**, meaning every variable has a specific **data type**. However, Dart supports **type inference**, so you don't always need to explicitly mention types.

---

### ✅ 1. **Numbers**

Dart has two main types for numbers:

* `int` – for whole numbers
* `double` – for decimal numbers (floating-point)

```dart
int age = 25;
double pi = 3.1415;
```

You can also use:

```dart
num x = 10;   // Can hold both int and double
x = 10.5;
```

---

### ✅ 2. **Strings**

Used to represent text. Strings are enclosed in **single** or **double** quotes.

```dart
String name = 'Uday';
String greeting = "Hello, $name!";
```

* **String interpolation**:

  ```dart
  print("Age is ${age + 5}");
  ```

---

### ✅ 3. **Booleans**

The `bool` type represents two values: `true` or `false`.

```dart
bool isLoggedIn = true;
```

Used in conditionals:

```dart
if (isLoggedIn) {
  print("Welcome back!");
}
```

---

### ✅ 4. **Lists (Arrays)**

A **List** is an ordered group of objects.

```dart
List<int> numbers = [1, 2, 3];
var names = ['Alice', 'Bob'];
```

* Access element: `numbers[0]`
* Add item: `numbers.add(4);`

---

### ✅ 5. **Maps**

A **Map** is a collection of key-value pairs.

```dart
Map<String, String> user = {
  'name': 'Uday',
  'email': 'uday@example.com'
};

print(user['name']);  // Uday
```

---

### ✅ 6. **Sets**

A **Set** is an unordered collection of unique items.

```dart
Set<int> uniqueNumbers = {1, 2, 3, 2};
print(uniqueNumbers); // {1, 2, 3}
```

---

### ✅ 7. **Runes**

Used to represent Unicode characters.

```dart
var heart = '\u2665';  // ♥
```

---

### ✅ 8. **Symbols**

Symbols are used for **reflection** and meta-programming.

```dart
Symbol s = #myFunction;
```

---

### ✅ 9. **Dynamic**

Used when the variable type is not known at compile time.

```dart
dynamic something = 'hello';
something = 10; // valid
```

---

### ✅ 10. **var vs final vs const**

* `var` – Type inferred at runtime.
* `final` – Value set only once.
* `const` – Compile-time constant.

```dart
var a = 10;
final b = 20;
const c = 30;
```

---

### ✅ 11. **Object**

Everything in Dart is an **object**, and all classes inherit from the `Object` class.

```dart
Object value = "String as object";
```

---

