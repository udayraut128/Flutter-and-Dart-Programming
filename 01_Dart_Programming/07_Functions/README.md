### 🟢 **Topic 7: Functions in Dart**

A **function** is a block of code that performs a specific task. Dart treats functions as **first-class objects**, meaning you can assign them to variables, pass them as arguments, and return them from other functions.

---

### ✅ 1. **Basic Function Syntax**

```dart
void greet() {
  print("Hello!");
}

void main() {
  greet(); // Calling the function
}
```

---

### ✅ 2. **Function with Parameters**

```dart
void greetUser(String name) {
  print("Hello, $name!");
}
```

---

### ✅ 3. **Function with Return Value**

```dart
int add(int a, int b) {
  return a + b;
}
```

---

### ✅ 4. **Optional Positional Parameters**

Use `[]` to make parameters optional.

```dart
void showInfo(String name, [int? age]) {
  print("Name: $name");
  if (age != null) print("Age: $age");
}
```

---

### ✅ 5. **Optional Named Parameters**

Use `{}` to make parameters optional and **named**.

```dart
void showDetails({String? name, int? age}) {
  print("Name: $name, Age: $age");
}
```

* With default values:

```dart
void showDetails({String name = "Guest", int age = 0}) {
  print("Name: $name, Age: $age");
}
```

---

### ✅ 6. **Required Named Parameters**

Use `required` keyword:

```dart
void display({required String title}) {
  print("Title: $title");
}
```

---

### ✅ 7. **Arrow Functions (Fat Arrow `=>`)**

Used for short one-line functions.

```dart
int square(int x) => x * x;
```

---

### ✅ 8. **Anonymous Functions**

Functions without a name. Often used in callbacks.

```dart
var list = [1, 2, 3];
list.forEach((item) {
  print(item);
});
```

---

### ✅ 9. **Higher-Order Functions**

Functions that:

* Accept functions as parameters, or
* Return functions

```dart
void operate(int a, int b, Function f) {
  print(f(a, b));
}

int add(int x, int y) => x + y;

void main() {
  operate(5, 3, add); // Output: 8
}
```

---

### ✅ 10. **Function as First-Class Object**

Assign function to a variable:

```dart
int multiply(int a, int b) => a * b;

void main() {
  var op = multiply;
  print(op(3, 4)); // 12
}
```

---

### ✅ 11. **Recursion**

A function that calls itself.

```dart
int factorial(int n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}
```

---

### ✅ 12. **Closures**

A closure captures variables from its surrounding scope.

```dart
Function counter() {
  int count = 0;
  return () {
    count++;
    print(count);
  };
}

void main() {
  var c = counter();
  c(); // 1
  c(); // 2
}
```

---

### Summary

| Concept              | Example/Keyword |
| -------------------- | --------------- |
| Function declaration | `void func()`   |
| Return type          | `int add()`     |
| Optional parameters  | `[int? x]`      |
| Named parameters     | `{int? y}`      |
| Required named param | `required`      |
| Arrow function       | `=>`            |
| Anonymous function   | `(x) {}`        |
| Higher-order func    | `Function f`    |
| Recursion            | Calls itself    |
| Closure              | Captures state  |

---

