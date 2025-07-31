### 🟢 **Topic 9: Exception Handling in Dart**

**Exception handling** allows you to gracefully manage runtime errors, ensuring that your app doesn’t crash unexpectedly.

---

### ✅ 1. **What is an Exception?**

An **exception** is an **error** that occurs during program execution. Dart provides a powerful mechanism to handle these errors using:

* `try`
* `catch`
* `on`
* `finally`
* `throw`

---

### ✅ 2. **try-catch Block**

Use `try-catch` to catch and handle exceptions.

```dart
void main() {
  try {
    int result = 10 ~/ 0; // Will throw an exception
    print(result);
  } catch (e) {
    print("Error: $e");
  }
}
```

Output:

```
Error: IntegerDivisionByZeroException
```

---

### ✅ 3. **try-on-catch**

Use `on` to catch **specific exception types**.

```dart
void main() {
  try {
    int result = 10 ~/ 0;
    print(result);
  } on IntegerDivisionByZeroException {
    print("You can't divide by zero!");
  } catch (e) {
    print("Unknown error: $e");
  }
}
```

---

### ✅ 4. **catch with Stack Trace**

Use a second parameter to capture the **stack trace**.

```dart
void main() {
  try {
    throw FormatException("Invalid format");
  } catch (e, s) {
    print("Exception: $e");
    print("Stack trace:\n$s");
  }
}
```

---

### ✅ 5. **finally Block**

`finally` runs **regardless** of whether an exception occurred.

```dart
void main() {
  try {
    int result = 10 ~/ 2;
    print(result);
  } catch (e) {
    print("Error: $e");
  } finally {
    print("Cleanup done.");
  }
}
```

---

### ✅ 6. **throw Keyword**

You can **manually throw exceptions**.

```dart
void checkAge(int age) {
  if (age < 18) {
    throw Exception("Underage");
  } else {
    print("Welcome!");
  }
}

void main() {
  try {
    checkAge(16);
  } catch (e) {
    print("Caught: $e");
  }
}
```

---

### ✅ 7. **Custom Exceptions**

You can create your own exception classes by extending `Exception` or `Error`.

```dart
class NegativeAmountException implements Exception {
  String errorMessage() => 'Amount can’t be negative';
}

void withdraw(int amount) {
  if (amount < 0) {
    throw NegativeAmountException();
  }
}

void main() {
  try {
    withdraw(-100);
  } catch (e) {
    print(e.errorMessage());
  }
}
```

---

### ✅ Summary Table

| Keyword   | Purpose                                     |
| --------- | ------------------------------------------- |
| `try`     | Contains code that might throw an exception |
| `catch`   | Catches general or specific exceptions      |
| `on`      | Catches specific exception types            |
| `finally` | Always runs, used for cleanup               |
| `throw`   | Manually throw an exception                 |

---

### 🧪 Real-Life Example

```dart
void divideNumbers(int a, int b) {
  try {
    double result = a / b;
    print("Result: $result");
  } on IntegerDivisionByZeroException {
    print("You can't divide by zero!");
  } catch (e) {
    print("Unknown error: $e");
  } finally {
    print("End of operation");
  }
}

void main() {
  divideNumbers(10, 0);
}
```

---

