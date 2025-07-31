## 🟢 **Topic 10: Collections in Dart (Lists, Sets, and Maps)**

Collections are used to store **multiple values** in a single variable. Dart provides **three main types** of collections:

1. **List** (ordered collection)
2. **Set** (unordered and unique)
3. **Map** (key-value pairs)

---

### ✅ 1. **List**

A **List** is an ordered group of items. It’s like an array in other languages.

#### 🔹 Declaration & Initialization

```dart
List<String> fruits = ['Apple', 'Banana', 'Mango'];
```

#### 🔹 Access Elements

```dart
print(fruits[0]); // Apple
```

#### 🔹 Add Items

```dart
fruits.add('Orange');
```

#### 🔹 Remove Items

```dart
fruits.remove('Banana');
```

#### 🔹 Iterate List

```dart
for (var fruit in fruits) {
  print(fruit);
}
```

#### 🔹 List Properties

```dart
print(fruits.length);
print(fruits.isEmpty);
print(fruits.contains('Apple'));
```

#### 🔹 Spread Operator (…)

```dart
var list1 = [1, 2, 3];
var list2 = [0, ...list1, 4]; // [0, 1, 2, 3, 4]
```

#### 🔹 Null-aware Spread

```dart
List<int>? a;
var b = [0, ...?a]; // [0]
```

---

### ✅ 2. **Set**

A **Set** is an unordered collection of **unique** items (no duplicates).

#### 🔹 Declaration

```dart
Set<int> numbers = {1, 2, 3};
```

#### 🔹 Add/Remove Elements

```dart
numbers.add(4);
numbers.remove(2);
```

#### 🔹 Check Membership

```dart
print(numbers.contains(3));
```

#### 🔹 Iterating

```dart
for (var num in numbers) {
  print(num);
}
```

---

### ✅ 3. **Map**

A **Map** is a collection of **key-value pairs**.

#### 🔹 Declaration

```dart
Map<String, String> capital = {
  'India': 'Delhi',
  'USA': 'Washington',
};
```

#### 🔹 Access/Update Values

```dart
print(capital['India']); // Delhi
capital['USA'] = 'New York'; // Update
```

#### 🔹 Add/Remove Elements

```dart
capital['Japan'] = 'Tokyo';
capital.remove('India');
```

#### 🔹 Iterate Map

```dart
capital.forEach((key, value) {
  print('$key → $value');
});
```

#### 🔹 Map Properties

```dart
print(capital.length);
print(capital.keys);
print(capital.values);
```

---

### ✅ 4. **Collection if/for (Collection Control Flow)**

Dart supports conditional collection building.

#### 🔹 if

```dart
var promoActive = true;
var nav = ['Home', 'About', if (promoActive) 'Promo'];
```

#### 🔹 for

```dart
var nums = [1, 2, 3];
var squares = [for (var n in nums) n * n]; // [1, 4, 9]
```

---

### 🧪 Real-Life Example: Student Info with List, Set, and Map

```dart
void main() {
  List<String> students = ['Alice', 'Bob', 'Charlie'];
  Set<String> enrolled = {'Bob', 'Charlie'};
  Map<String, int> scores = {'Alice': 90, 'Bob': 85, 'Charlie': 88};

  for (var student in students) {
    if (enrolled.contains(student)) {
      print('$student is enrolled with score ${scores[student]}');
    } else {
      print('$student is not enrolled');
    }
  }
}
```

---

### ✅ Summary Table

| Collection | Ordered | Duplicates  | Example            |
| ---------- | ------- | ----------- | ------------------ |
| List       | Yes     | Yes         | `['a', 'b', 'c']`  |
| Set        | No      | No          | `{1, 2, 3}`        |
| Map        | N/A     | Unique Keys | `{'key': 'value'}` |

---
 