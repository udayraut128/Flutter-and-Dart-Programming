### 🟢 **Topic 8: Object-Oriented Programming (OOP) in Dart**

Dart is a **fully object-oriented language**: everything is an object and inherits from the `Object` class. OOP makes your code modular, reusable, and easier to manage using **Classes**, **Objects**, **Inheritance**, **Polymorphism**, and **Abstraction**.

---

## ✅ 1. **Class and Object**

### 🔹 Class: Blueprint for creating objects (data + behavior).

### 🔹 Object: Instance of a class.

```dart
class Car {
  String brand = 'Ford';

  void drive() {
    print("Driving a $brand car.");
  }
}

void main() {
  Car myCar = Car();     // Creating an object
  myCar.drive();         // Calling method
}
```

---

## ✅ 2. **Constructors**

Constructors are special methods to initialize objects.

### 🔹 Default Constructor

```dart
class Student {
  Student() {
    print("Constructor called!");
  }
}
```

### 🔹 Parameterized Constructor

```dart
class Student {
  String name;
  int age;

  Student(this.name, this.age);

  void display() {
    print("Name: $name, Age: $age");
  }
}
```

---

## ✅ 3. **Named Constructors**

Used to create multiple constructors with names.

```dart
class Student {
  String name = "";
  int age = 0;

  Student.named(String n, int a) {
    name = n;
    age = a;
  }
}
```

---

## ✅ 4. **Constant Constructor**

For creating compile-time constant objects.

```dart
class Point {
  final int x, y;

  const Point(this.x, this.y);
}

void main() {
  const p1 = Point(1, 2);
}
```

---

## ✅ 5. **this Keyword**

Refers to the current class instance.

```dart
class Person {
  String name;

  Person(this.name); // this.name = name (auto-assigned)
}
```

---

## ✅ 6. **Getters and Setters**

Used to access or update private variables.

```dart
class Circle {
  double _radius = 0;

  double get radius => _radius;

  set radius(double value) {
    if (value > 0) {
      _radius = value;
    }
  }
}
```

---

## ✅ 7. **Static Members**

Belong to the class, not the object.

```dart
class Counter {
  static int count = 0;

  static void increment() {
    count++;
  }
}
```

Call using: `Counter.increment();`

---

## ✅ 8. **Inheritance**

Allows one class to inherit from another.

```dart
class Animal {
  void speak() {
    print("Animal speaks");
  }
}

class Dog extends Animal {
  void bark() {
    print("Dog barks");
  }
}
```

Use:

```dart
Dog d = Dog();
d.speak(); // inherited
d.bark();  // own method
```

---

## ✅ 9. **Method Overriding**

Child class overrides parent method.

```dart
class Animal {
  void sound() {
    print("Some sound");
  }
}

class Cat extends Animal {
  @override
  void sound() {
    print("Meow");
  }
}
```

---

## ✅ 10. **Abstract Classes**

Cannot be instantiated. Used as base classes with abstract methods.

```dart
abstract class Shape {
  void draw(); // abstract method
}

class Circle extends Shape {
  @override
  void draw() {
    print("Drawing circle");
  }
}
```

---

## ✅ 11. **Interfaces**

Every class in Dart can be used as an interface.

```dart
class Printer {
  void printData() => print("Printing...");
}

class Scanner {
  void scanData() => print("Scanning...");
}

class AllInOne implements Printer, Scanner {
  @override
  void printData() => print("All-in-One Print");

  @override
  void scanData() => print("All-in-One Scan");
}
```

---

## ✅ 12. **Mixins**

For sharing code across multiple classes **without inheritance**.

```dart
mixin Logger {
  void log(String msg) => print("LOG: $msg");
}

class Service with Logger {}

void main() {
  var s = Service();
  s.log("Started");
}
```

---

## ✅ 13. **Enums**

A fixed set of named values.

```dart
enum Status { success, failure, pending }

void main() {
  Status s = Status.success;
  print(s); // Status.success
}
```

---

## ✅ 14. **Extension Methods**

Add functionality to existing classes.

```dart
extension StringExtension on String {
  String reverse() => split('').reversed.join();
}

void main() {
  print("Dart".reverse()); // traD
}
```

---

## ✅ Summary Table

| Feature        | Keyword/Concept             |
| -------------- | --------------------------- |
| Class & Object | `class`, `new`              |
| Constructor    | `ClassName()`, `this`       |
| Inheritance    | `extends`                   |
| Overriding     | `@override`                 |
| Abstract Class | `abstract`                  |
| Interface      | `implements`                |
| Mixin          | `mixin`, `with`             |
| Static Members | `static`                    |
| Encapsulation  | `_private`, getters/setters |
| Enums          | `enum`                      |
| Extensions     | `extension`                 |

---

### 🧪 Example Scenario:

```dart
abstract class Vehicle {
  void move();
}

mixin Engine {
  void start() => print("Engine started");
}

class Car extends Vehicle with Engine {
  @override
  void move() {
    print("Car is moving");
  }
}

void main() {
  Car c = Car();
  c.start(); // Engine started
  c.move();  // Car is moving
}
```

---
 
