## 🔷 1. **SharedPreferences**

### 📌 What is it?

* Used to **store simple key-value pairs**
* Works best for **small data** (e.g., login status, theme settings)
* Data is stored persistently on device

### ✅ Use Case:

* Save user’s theme preference (dark/light)
* Remember login state

### 🧪 Example 1: Save & Get a Boolean

```dart
final prefs = await SharedPreferences.getInstance();
await prefs.setBool('isLoggedIn', true);

bool? isLoggedIn = prefs.getBool('isLoggedIn');
print(isLoggedIn); // true
```

### 🧪 Example 2: Save & Get a String

```dart
await prefs.setString('username', 'udayraut128');

String? name = prefs.getString('username');
```

---

## 🔷 2. **SQLite (sqflite package)**

### 📌 What is it?

* A full **relational database** (SQL-based)
* Best for **structured, relational data**
* Ideal when you need queries, joins, etc.

### ✅ Use Case:

* Storing notes, tasks, offline data

### 🧪 Example 1: Setup Table

```dart
Database db = await openDatabase('notes.db', version: 1,
  onCreate: (db, version) async {
    await db.execute('''
      CREATE TABLE notes (
        id INTEGER PRIMARY KEY,
        title TEXT,
        content TEXT
      )
    ''');
});
```

### 🧪 Example 2: Insert & Retrieve

```dart
await db.insert('notes', {'title': 'Note 1', 'content': 'Hello world'});
List<Map<String, dynamic>> results = await db.query('notes');

print(results); // [{id: 1, title: Note 1, content: Hello world}]
```

---

## 🔷 3. **ObjectBox / Hive**

### 📌 What is it?

* **NoSQL** data storage (fast, key-value, object-boxed)
* Hive is lightweight, ObjectBox is faster with relations

### ✅ Use Case:

* Store large amounts of **non-relational** data
* Offline-first apps

---

### ✅ Hive Setup:

```yaml
dependencies:
  hive: ^2.0.0
  hive_flutter: ^1.0.0
```

---

### 🧪 Example 1: Hive Initialization & Box

```dart
await Hive.initFlutter();
var box = await Hive.openBox('settings');
await box.put('isDarkMode', true);

bool isDark = box.get('isDarkMode');
```

---

### 🧪 Example 2: Store Custom Object (Hive + Adapter)

```dart
@HiveType(typeId: 0)
class Task extends HiveObject {
  @HiveField(0)
  String title;

  @HiveField(1)
  bool done;
}
```

---

### ✅ ObjectBox:

* Faster than Hive, supports queries and relationships
* Great for real-time reactive databases

---

## 🔷 4. **File Storage**

### 📌 What is it?

* Save files as **text, images, or binary data**
* Stored inside app’s **internal or external directory**

### ✅ Use Case:

* Save logs, documents, media

### 🧪 Example 1: Write and Read a File

```dart
import 'dart:io';
import 'package:path_provider/path_provider.dart';

Future<File> getFile() async {
  final dir = await getApplicationDocumentsDirectory();
  return File('${dir.path}/userdata.txt');
}

void writeToFile(String content) async {
  final file = await getFile();
  await file.writeAsString(content);
}

Future<String> readFile() async {
  final file = await getFile();
  return await file.readAsString();
}
```

---

## 🔷 5. **Secure Storage (`flutter_secure_storage`)**

### 📌 What is it?

* Stores sensitive data securely using **Android Keystore / iOS Keychain**
* Encrypts data automatically

### ✅ Use Case:

* Storing **tokens**, **passwords**, **PINs**, **session info**

### 🧪 Setup:

```yaml
dependencies:
  flutter_secure_storage: ^9.0.0
```

---

### 🧪 Example 1: Save & Read Securely

```dart
final storage = new FlutterSecureStorage();

// Write
await storage.write(key: 'token', value: 'abcd1234');

// Read
String? token = await storage.read(key: 'token');
print(token);
```

---

### 🧪 Example 2: Delete Secure Key

```dart
await storage.delete(key: 'token');
```

---

## 🔚 Summary Table

| Method             | Best For                      | Persistent | Secure | Structured |
| ------------------ | ----------------------------- | ---------- | ------ | ---------- |
| SharedPreferences  | Simple key-value              | ✅          | ❌      | ❌          |
| SQLite (`sqflite`) | Complex relational data       | ✅          | ❌      | ✅          |
| Hive/ObjectBox     | Large data, fast NoSQL        | ✅          | ❌      | ❌ / ✅      |
| File Storage       | Logs, Text/Images             | ✅          | ❌      | ❌          |
| Secure Storage     | Sensitive (passwords, tokens) | ✅          | ✅      | ❌          |

---
 
