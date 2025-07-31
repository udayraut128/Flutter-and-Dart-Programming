### 📌 What is a Typedef?

A **typedef** in Dart is a way to **create an alias for a function type**. It improves **readability**, helps in **callback definitions**, and promotes **cleaner code**, especially with complex function signatures.

---

## 🔹 16.1: Function Aliases

### 🔸 Basic Syntax

```dart
typedef MyFunction = void Function(String name);
```

This means: `MyFunction` is now an alias for any function that takes a `String` and returns `void`.

### 🔸 Example

```dart
typedef Greet = void Function(String name);

void sayHello(String name) {
  print('Hello, $name!');
}

void greetUser(Greet greetFunc) {
  greetFunc('Uday');
}

void main() {
  greetUser(sayHello);
}
```

🟢 Output: `Hello, Uday!`

---

## 🔹 16.2: Generic Typedefs

You can use generics with typedefs too.

```dart
typedef Transformer<T> = T Function(T value);

T apply<T>(T value, Transformer<T> transformer) {
  return transformer(value);
}

void main() {
  int doubled = apply<int>(5, (x) => x * 2);
  print(doubled); // Output: 10

  String upper = apply<String>("dart", (x) => x.toUpperCase());
  print(upper); // Output: DART
}
```

---

## ✅ When to Use Typedefs

| Use Case                 | Benefit                              |
| ------------------------ | ------------------------------------ |
| ✅ Callback functions     | Improves readability                 |
| ✅ Event handlers         | Makes signatures clear               |
| ✅ Reusability            | Type aliases reduce redundancy       |
| ✅ Complex function types | Keeps the code clean and easy to use |

---

## 🔸 Without Typedef vs With Typedef

🔻 Without typedef:

```dart
void greet(void Function(String) greetFunc) {
  greetFunc("World");
}
```

✅ With typedef:

```dart
typedef GreetFunction = void Function(String);

void greet(GreetFunction greetFunc) {
  greetFunc("World");
}
```

---

## 🧠 Summary

* Use `typedef` to define a **name** for a **function type**.
* It helps with **callbacks**, **clean code**, and **readability**.
* You can create **generic typedefs** for flexible code.

---
 