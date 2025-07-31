## 🔷 What is JSON?

**JSON (JavaScript Object Notation)** is a lightweight data format used for storing and exchanging data.

Flutter often uses JSON to **communicate with APIs**, **store config files**, or **work with local data**.

---

## 🔹 1. **Parsing JSON**

JSON parsing means converting JSON strings to **Dart objects** and vice versa.

### 🧪 Example JSON Response:

```json
{
  "id": 1,
  "name": "Uday Raut",
  "email": "uday@example.com"
}
```

---

## 🔹 2. **Manual Parsing**

### ✅ Step-by-step:

#### 🔸 Model Class:

```dart
class User {
  final int id;
  final String name;
  final String email;

  User({required this.id, required this.name, required this.email});

  // fromJson factory
  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'],
      name: json['name'],
      email: json['email'],
    );
  }

  // toJson method
  Map<String, dynamic> toJson() => {
        'id': id,
        'name': name,
        'email': email,
      };
}
```

#### 🔸 Parsing JSON String:

```dart
String jsonString = '{"id":1,"name":"Uday Raut","email":"uday@example.com"}';
Map<String, dynamic> userMap = jsonDecode(jsonString);

User user = User.fromJson(userMap);
print(user.name); // Uday Raut
```

---

### 🧪 Example 2: List of Users

```dart
String jsonList = '''
[
  {"id":1,"name":"Uday"},
  {"id":2,"name":"Ravi"}
]
''';

List<dynamic> data = jsonDecode(jsonList);
List<User> users = data.map((e) => User.fromJson(e)).toList();

print(users[1].name); // Ravi
```

---

## 🔹 3. **fromJson and toJson Methods**

* `fromJson(Map<String, dynamic> json)` — Converts JSON to Dart object.
* `toJson()` — Converts Dart object to JSON.

These methods are essential for data exchange.

### ✅ Example Usage:

```dart
User user = User(id: 5, name: "Test", email: "test@example.com");
String userJson = jsonEncode(user.toJson());

print(userJson);
// {"id":5,"name":"Test","email":"test@example.com"}
```

---

## 🔹 4. **Using `json_serializable` Package**

This package **automates** `fromJson` and `toJson` generation via annotations.

### ✅ Step 1: Add dependencies in `pubspec.yaml`

```yaml
dependencies:
  json_annotation: ^4.8.1

dev_dependencies:
  build_runner: ^2.4.7
  json_serializable: ^6.7.1
```

---

### ✅ Step 2: Create Model Class

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart'; // Generated file

@JsonSerializable()
class User {
  final int id;
  final String name;
  final String email;

  User({required this.id, required this.name, required this.email});

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

---

### ✅ Step 3: Run Build Runner

```bash
flutter pub run build_runner build
```

This generates `user.g.dart` with fromJson & toJson logic.

---

### 🧪 Example:

```dart
String data = '{"id":2,"name":"Ankit","email":"ankit@example.com"}';
User user = User.fromJson(jsonDecode(data));

print(user.name); // Ankit
```

---

## 🔚 Summary Table

| Method               | Description                           | Best Use Case                         |
| -------------------- | ------------------------------------- | ------------------------------------- |
| Manual Parsing       | Write fromJson & toJson manually      | Small projects, full control          |
| `fromJson`, `toJson` | Converts between Dart & JSON          | Essential for data model conversion   |
| `json_serializable`  | Auto-generate fromJson/toJson methods | Medium/large apps, scalable structure |

---

## ✅ Final Tips:

* Use `jsonDecode` / `jsonEncode` from `dart:convert` package.
* Always check for `null` fields or missing keys.
* Use `json_serializable` to reduce errors and boilerplate code.

---
 