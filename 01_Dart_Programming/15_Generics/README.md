## 🟪 **Topic 15: Generics in Dart**

---

### 📌 What Are Generics?

**Generics** allow you to write **flexible**, **reusable**, and **type-safe** code. Instead of hardcoding types, you use **type parameters**, which can work with any data type.

---

### ✅ Why Use Generics?

Without generics:

```dart
List names = ['Alice', 'Bob'];
names.add(123); // No error, but incorrect type.
```

With generics:

```dart
List<String> names = ['Alice', 'Bob'];
names.add(123); // ❌ Error: value of type 'int' can't be assigned to 'String'
```

✅ Ensures **type safety** and **compiler checks**.

---

## 🔹 15.1: Generic Functions

### 🔸 Syntax:

```dart
T functionName<T>(T param) {
  return param;
}
```

### 🔸 Example:

```dart
T echo<T>(T value) {
  return value;
}

void main() {
  print(echo<String>("Hello"));  // Output: Hello
  print(echo<int>(42));          // Output: 42
}
```

---

## 🔹 15.2: Generic Classes

### 🔸 Syntax:

```dart
class Box<T> {
  T value;
  Box(this.value);

  void show() => print("Value: $value");
}
```

### 🔸 Usage:

```dart
void main() {
  Box<String> strBox = Box("Dart");
  strBox.show(); // Output: Value: Dart

  Box<int> intBox = Box(100);
  intBox.show(); // Output: Value: 100
}
```

---

## 🔹 15.3: Constraints on Generics

Use `extends` to limit which types can be used.

```dart
class Animal {
  void sound() => print("Some sound");
}

class Dog extends Animal {
  void sound() => print("Bark!");
}

class AnimalBox<T extends Animal> {
  T animal;
  AnimalBox(this.animal);
  void makeSound() => animal.sound();
}

void main() {
  var dogBox = AnimalBox(Dog());
  dogBox.makeSound(); // Output: Bark!
}
```

✅ This restricts the generic type to only **Animal** or its **subclasses**.

---

## 🔸 Benefits of Generics in Dart

| Benefit            | Description                                |
| ------------------ | ------------------------------------------ |
| 🔐 Type Safety     | Catch errors at compile time               |
| 🔁 Reusability     | Write code that works with many data types |
| 🚀 Performance     | Avoid unnecessary type checks and casts    |
| 📦 Maintainability | Cleaner, scalable code                     |

---

## 🧠 Summary

* Use `<T>` to define generic types.
* Generics can be used in **functions**, **classes**, and even **collections**.
* You can **restrict types** using `extends`.

---
 
