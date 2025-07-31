## 📦 1. Using `pubspec.yaml`

### ✅ Purpose:

`pubspec.yaml` is the **configuration file** where you define:

* App metadata (name, version)
* Dependencies (external packages)
* Assets
* Fonts

---

### 🔸 Structure Example:

```yaml
name: my_app
description: A new Flutter project.
version: 1.0.0+1

dependencies:
  flutter:
    sdk: flutter
  http: ^1.2.0
  provider: ^6.0.5

flutter:
  assets:
    - assets/images/
  fonts:
    - family: Poppins
      fonts:
        - asset: fonts/Poppins-Regular.ttf
```

---

### 🧪 Examples:

#### ✅ Example 1: Adding a package

```yaml
dependencies:
  url_launcher: ^6.2.4
```

#### ✅ Example 2: Adding assets

```yaml
flutter:
  assets:
    - images/logo.png
```

#### ✅ Example 3: Adding fonts

```yaml
flutter:
  fonts:
    - family: Roboto
      fonts:
        - asset: fonts/Roboto-Regular.ttf
```

---

## 📥 2. Installing & Importing Packages

### ✅ Purpose:

After adding dependencies in `pubspec.yaml`, use:

* `flutter pub get` to install
* `import 'package:package_name/...'` to use it

---

### 🧪 Examples:

#### ✅ Example 1: Installing `http`

```bash
flutter pub add http
```

#### ✅ Example 2: Import in Dart file

```dart
import 'package:http/http.dart' as http;
```

#### ✅ Example 3: Use after import

```dart
final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));
print(response.body);
```

#### ✅ Example 4: Auto install after modifying `pubspec.yaml`

```bash
flutter pub get
```

---

## 🌟 3. Popular Packages in Flutter

### ✅ 1. `url_launcher`

Used to open URLs, phone dialer, email, etc.

```yaml
dependencies:
  url_launcher: ^6.2.4
```

```dart
import 'package:url_launcher/url_launcher.dart';

void launchWeb() async {
  final Uri url = Uri.parse('https://flutter.dev');
  if (!await launchUrl(url)) {
    throw 'Could not launch $url';
  }
}
```

---

### ✅ 2. `path_provider`

Used to get system directories (documents, temp, etc.)

```yaml
dependencies:
  path_provider: ^2.1.1
```

```dart
import 'package:path_provider/path_provider.dart';
import 'dart:io';

void saveFile() async {
  final dir = await getApplicationDocumentsDirectory();
  final file = File('${dir.path}/demo.txt');
  await file.writeAsString('Flutter is awesome!');
}
```

---

### ✅ 3. `shared_preferences`

Used for local key-value storage.

```yaml
dependencies:
  shared_preferences: ^2.2.1
```

```dart
import 'package:shared_preferences/shared_preferences.dart';

void saveUsername() async {
  final prefs = await SharedPreferences.getInstance();
  prefs.setString('username', 'udayraut128');
}
```

---

### ✅ 4. `provider`

Used for state management.

```yaml
dependencies:
  provider: ^6.1.1
```

```dart
import 'package:provider/provider.dart';

class Counter with ChangeNotifier {
  int value = 0;
  void increment() {
    value++;
    notifyListeners();
  }
}
```

---

## 🛠️ 4. Creating Custom Packages

### ✅ Purpose:

You can create your **own reusable packages** for internal libraries, custom widgets, utilities, etc.

---

### 🔸 Steps:

#### ✅ Step 1: Create a package

```bash
flutter create --template=package my_custom_package
```

---

#### ✅ Step 2: Project structure

```
my_custom_package/
 ├─ lib/
 │   └─ my_custom_package.dart
 └─ pubspec.yaml
```

---

#### ✅ Step 3: Define package logic

```dart
// lib/my_custom_package.dart
library my_custom_package;

String greet(String name) => 'Hello, $name!';
```

---

#### ✅ Step 4: Use in another app

1. Local path in pubspec.yaml:

```yaml
dependencies:
  my_custom_package:
    path: ../my_custom_package
```

2. Import and use:

```dart
import 'package:my_custom_package/my_custom_package.dart';

void main() {
  print(greet("Uday")); // Hello, Uday!
}
```

---

### 🧪 Example Use Cases:

#### ✅ Example 1: Custom math utilities

```dart
int square(int x) => x * x;
```

#### ✅ Example 2: Custom widgets (like `CustomButton`)

```dart
class CustomButton extends StatelessWidget { ... }
```

#### ✅ Example 3: Common API service

```dart
class ApiService {
  Future<dynamic> get(String url) {...}
}
```

#### ✅ Example 4: Shared themes across apps

```dart
ThemeData customTheme = ThemeData(primarySwatch: Colors.teal);
```

---

## ✅ Summary

| Topic                    | Description                                             | Example                             |
| ------------------------ | ------------------------------------------------------- | ----------------------------------- |
| `pubspec.yaml`           | Manages dependencies, assets, fonts                     | `http`, `assets/images/`            |
| Installing & Importing   | Add via `pub`, import in Dart file                      | `flutter pub add`, `import`         |
| Popular Packages         | Useful tools for web, files, storage, UI, state         | `url_launcher`, `provider`          |
| Creating Custom Packages | Build reusable code libraries for your team or yourself | `flutter create --template=package` |

---

 
