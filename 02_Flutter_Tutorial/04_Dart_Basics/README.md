# 🎯 4. Dart Basics (for Flutter)

---

## 🧮 1. **Variables, Data Types, Operators**

### ✅ Variables in Dart

Variables store data. Dart is a statically typed language but allows both explicit and implicit types.

```dart
// Explicit typing
int age = 25;

// Implicit typing (type inferred)
var name = 'Uday';
```

### 🔐 Final and Const

```dart
final city = 'Mumbai'; // Set only once at runtime
const PI = 3.14;       // Set at compile time
```

### ✅ Data Types

| Type      | Example                                 |
| --------- | --------------------------------------- |
| `int`     | `int x = 10;`                           |
| `double`  | `double pi = 3.14;`                     |
| `String`  | `String name = 'Uday';`                 |
| `bool`    | `bool isTrue = true;`                   |
| `List`    | `List<int> nums = [1,2];`               |
| `Map`     | `Map<String, int> ages = {'Uday': 25};` |
| `dynamic` | `dynamic x = 5; x = 'hi';`              |

### ✅ Operators

* **Arithmetic**: `+`, `-`, `*`, `/`, `~/` (integer div), `%`
* **Comparison**: `==`, `!=`, `<`, `>`, `<=`, `>=`
* **Logical**: `&&`, `||`, `!`
* **Assignment**: `=`, `+=`, `-=`, `*=`, etc.
* **Null-aware**:

  ```dart
  var name = userName ?? 'Guest';  // if userName is null
  ```

---

## 🔁 2. **Control Flow (if, switch, loops)**

### ✅ if-else

```dart
if (age > 18) {
  print('Adult');
} else {
  print('Minor');
}
```

### ✅ switch-case

```dart
switch (day) {
  case 'Monday':
    print('Start of week');
    break;
  default:
    print('Unknown day');
}
```

### ✅ Loops

```dart
// for loop
for (int i = 0; i < 5; i++) {
  print(i);
}

// while loop
int i = 0;
while (i < 5) {
  print(i++);
}

// do-while loop
int j = 0;
do {
  print(j++);
} while (j < 5);
}
```

---

## 🧮 3. **Functions**

Functions are reusable blocks of code.

### ✅ Basic Function

```dart
void greet() {
  print('Hello!');
}
```

### ✅ With Parameters

```dart
int add(int a, int b) {
  return a + b;
}
```

### ✅ Optional & Named Parameters

```dart
void greetUser(String name, {String prefix = 'Mr.'}) {
  print('Hello $prefix $name');
}

greetUser('Uday');              // Hello Mr. Uday
greetUser('Raut', prefix: 'Dr'); // Hello Dr Raut
```

### ✅ Arrow Function

```dart
int square(int x) => x * x;
```

---

## 🧱 4. **OOP in Dart (Classes, Objects, Inheritance)**

### ✅ Class and Object

```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  void greet() {
    print('Hi, I am $name and I am $age years old.');
  }
}

void main() {
  var p1 = Person('Uday', 25);
  p1.greet();
}
```

### ✅ Inheritance

```dart
class Animal {
  void sound() => print('Some sound');
}

class Dog extends Animal {
  @override
  void sound() => print('Bark');
}
```

### ✅ Getter/Setter

```dart
class Circle {
  double _radius;

  Circle(this._radius);

  double get area => 3.14 * _radius * _radius;

  set radius(double r) {
    if (r > 0) _radius = r;
  }
}
```

---

## ❓ 5. **Null Safety**

Null safety prevents runtime errors due to null values.

### ✅ Nullable & Non-Nullable

```dart
String name = 'Uday';        // non-nullable
String? nickname = null;     // nullable
```

### ✅ Null Check

```dart
if (nickname != null) {
  print(nickname.length);
}
```

### ✅ Null-aware Operators

| Operator | Use Case                     | Example                       |
| -------- | ---------------------------- | ----------------------------- |
| `??`     | Provide default if null      | `name = nickname ?? 'Guest';` |
| `?.`     | Call method only if not null | `nickname?.length`            |
| `??=`    | Assign if variable is null   | `nickname ??= 'Unknown';`     |

---

## ✅ Summary Table

| Concept      | Usage Example                          |
| ------------ | -------------------------------------- |
| Variable     | `var x = 10;`, `final name = 'John';`  |
| Data Type    | `int`, `String`, `List`, `Map`, `bool` |
| Function     | `void greet() {}`                      |
| Class/Object | `var p = Person();`                    |
| Inheritance  | `class Dog extends Animal`             |
| Null Safety  | `String? name`, `name ?? 'Guest'`      |

---

 