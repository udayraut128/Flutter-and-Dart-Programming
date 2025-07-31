## 🟩 **Topic 14: File I/O in Dart**

**File I/O (Input/Output)** allows your Dart program to **read from** and **write to** files, and **work with directories** — which is essential for apps that store logs, settings, or data.

This is done using the **`dart:io`** library (not supported on web).

---

### ✅ 14.1: Reading and Writing Files

#### 🔹 Import:

```dart
import 'dart:io';
```

---

### 📖 Reading from a File

#### ✅ Synchronously:

```dart
void main() {
  File file = File('example.txt');
  String contents = file.readAsStringSync();
  print(contents);
}
```

#### ✅ Asynchronously:

```dart
void main() async {
  File file = File('example.txt');
  String contents = await file.readAsString();
  print(contents);
}
```

---

### ✍ Writing to a File

#### ✅ Synchronously:

```dart
void main() {
  File file = File('example.txt');
  file.writeAsStringSync('Hello Dart!');
}
```

#### ✅ Asynchronously:

```dart
void main() async {
  File file = File('example.txt');
  await file.writeAsString('Hello Async Dart!');
}
```

---

### 📝 Appending to a File

```dart
void main() async {
  File file = File('example.txt');
  await file.writeAsString(' More text.', mode: FileMode.append);
}
```

---

### ✅ 14.2: Working with Directories

```dart
void main() {
  Directory dir = Directory('my_folder');

  if (!dir.existsSync()) {
    dir.createSync();
    print('Directory created!');
  } else {
    print('Directory already exists.');
  }
}
```

---

### ✅ 14.3: Asynchronous File Operations

Reading files line-by-line asynchronously:

```dart
void main() async {
  File file = File('example.txt');

  Stream<String> lines = file.openRead()
    .transform(utf8.decoder)
    .transform(LineSplitter());

  await for (var line in lines) {
    print('Line: $line');
  }
}
```

---

### 🔐 Other Useful Methods

| Method                      | Description                    |
| --------------------------- | ------------------------------ |
| `exists()` / `existsSync()` | Check if file/directory exists |
| `delete()` / `deleteSync()` | Delete file/directory          |
| `copy()`                    | Copy file                      |
| `rename()`                  | Rename or move file            |
| `list()`                    | List directory contents        |

---

### 📌 Notes

* File I/O requires **permissions** on some platforms.
* Avoid blocking the main thread: use **async** versions of methods.
* In **Flutter**, prefer using **path\_provider** for accessing device-specific paths.

---

 
