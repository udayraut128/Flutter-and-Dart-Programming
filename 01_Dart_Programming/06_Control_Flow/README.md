### 🟢 **Topic 6: Control Flow Statements in Dart**

Control flow statements **control the execution flow** of your program based on conditions and loops.

---

## ✅ 1. **if, else if, else**

Used to execute code based on conditions.

```dart
int age = 18;

if (age >= 18) {
  print("Adult");
} else if (age > 12) {
  print("Teen");
} else {
  print("Child");
}
```

---

## ✅ 2. **switch-case**

An alternative to multiple `if-else` statements. Best for discrete values.

```dart
var grade = 'B';

switch (grade) {
  case 'A':
    print("Excellent");
    break;
  case 'B':
    print("Good");
    break;
  case 'C':
    print("Average");
    break;
  default:
    print("Fail");
}
```

> 🔸 Don’t forget the `break` keyword to prevent fall-through behavior.

---

## ✅ 3. **for Loop**

Used when the number of iterations is known.

```dart
for (int i = 0; i < 5; i++) {
  print(i);
}
```

---

## ✅ 4. **while Loop**

Used when the number of iterations is **not known**, and you loop while a condition is true.

```dart
int i = 0;
while (i < 5) {
  print(i);
  i++;
}
```

---

## ✅ 5. **do-while Loop**

Executes at least once before checking the condition.

```dart
int i = 0;
do {
  print(i);
  i++;
} while (i < 5);
```

---

## ✅ 6. **break Statement**

Exits the loop or switch early.

```dart
for (int i = 0; i < 10; i++) {
  if (i == 5) break;
  print(i); // prints 0 to 4
}
```

---

## ✅ 7. **continue Statement**

Skips the current iteration and continues with the next one.

```dart
for (int i = 0; i < 5; i++) {
  if (i == 2) continue;
  print(i); // prints 0, 1, 3, 4
}
```

---

## ✅ 8. **Labels**

Used with break and continue to jump out of nested loops.

```dart
outerLoop:
for (int i = 0; i < 3; i++) {
  for (int j = 0; j < 3; j++) {
    if (i == 1 && j == 1) break outerLoop;
    print("i=$i, j=$j");
  }
}
```

---

### Summary Table

| Statement     | Use                                       |
| ------------- | ----------------------------------------- |
| `if`          | Checks a single condition                 |
| `if-else`     | Chooses between two conditions            |
| `else if`     | Checks multiple conditions in sequence    |
| `switch-case` | Best for matching against constant values |
| `for`         | Loop with a known number of iterations    |
| `while`       | Loops while a condition is true           |
| `do-while`    | Loop that runs at least once              |
| `break`       | Exit from loop or switch                  |
| `continue`    | Skip to next loop iteration               |
| `label:`      | Use with break/continue in nested loops   |

---
