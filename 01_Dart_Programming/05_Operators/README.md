### 🟢 **Topic 5: Operators in Dart**

Operators in Dart are used to perform operations on variables and values. Dart supports various types of operators just like other modern programming languages.

---

### ✅ 1. **Arithmetic Operators**

Used for basic mathematical operations.

| Operator | Description         | Example  |
| -------- | ------------------- | -------- |
| `+`      | Addition            | `a + b`  |
| `-`      | Subtraction         | `a - b`  |
| `*`      | Multiplication      | `a * b`  |
| `/`      | Division (double)   | `a / b`  |
| `~/`     | Integer Division    | `a ~/ b` |
| `%`      | Modulus (remainder) | `a % b`  |

```dart
int a = 10, b = 3;
print(a + b);  // 13
print(a ~/ b); // 3
print(a % b);  // 1
```

---

### ✅ 2. **Relational (Comparison) Operators**

Used to compare two values.

| Operator | Meaning                  |
| -------- | ------------------------ |
| `==`     | Equal to                 |
| `!=`     | Not equal to             |
| `>`      | Greater than             |
| `<`      | Less than                |
| `>=`     | Greater than or equal to |
| `<=`     | Less than or equal to    |

```dart
print(a == b);  // false
print(a > b);   // true
```

---

### ✅ 3. **Logical Operators**

Used for boolean logic.

| Operator | Meaning     |    |            |
| -------- | ----------- | -- | ---------- |
| `&&`     | Logical AND |    |            |
| \`       |             | \` | Logical OR |
| `!`      | Logical NOT |    |            |

```dart
bool x = true, y = false;
print(x && y);  // false
print(x || y);  // true
print(!x);      // false
```

---

### ✅ 4. **Bitwise Operators**

Operate on binary values.

| Operator | Meaning     |            |
| -------- | ----------- | ---------- |
| `&`      | Bitwise AND |            |
| \`       | \`          | Bitwise OR |
| `^`      | Bitwise XOR |            |
| `~`      | Bitwise NOT |            |
| `<<`     | Left shift  |            |
| `>>`     | Right shift |            |

```dart
print(5 & 3);  // 1
print(5 | 3);  // 7
```

---

### ✅ 5. **Assignment Operators**

Assign values to variables.

| Operator | Meaning             |
| -------- | ------------------- |
| `=`      | Assign              |
| `+=`     | Add and assign      |
| `-=`     | Subtract and assign |
| `*=`     | Multiply and assign |
| `/=`     | Divide and assign   |
| `%=`     | Modulus and assign  |

```dart
int a = 5;
a += 3;  // a = 8
```

---

### ✅ 6. **Type Test Operators**

Used to check or cast types.

| Operator | Meaning                              |
| -------- | ------------------------------------ |
| `is`     | True if object is of specified type  |
| `is!`    | False if object is of specified type |

```dart
print('Hello' is String);   // true
print(123 is! String);      // true
```

---

### ✅ 7. **Conditional Operators**

Used for concise conditional expressions.

#### a. Ternary operator:

```dart
condition ? expr1 : expr2
```

```dart
int age = 18;
print(age >= 18 ? 'Adult' : 'Minor');
```

#### b. Null-aware operator:

```dart
var name = username ?? 'Guest'; // If username is null, assign 'Guest'
```

---

### ✅ 8. **Cascade Notation (`..`)**

Used to perform multiple operations on the same object.

```dart
myObject
  ..method1()
  ..method2();
```

---

### ✅ 9. **Null-aware Operators**

| Operator | Meaning                        |
| -------- | ------------------------------ |
| `??`     | Default if null                |
| `??=`    | Assign only if null            |
| `?.`     | Safe access (only if not null) |

```dart
String? name;
print(name ?? 'Guest');    // Guest
name ??= 'Uday';           // assigns 'Uday' if name is null
```

---

### ✅ 10. **Increment / Decrement**

```dart
int a = 5;
a++;  // post-increment
++a;  // pre-increment
a--;  // post-decrement
--a;  // pre-decrement
```

---

