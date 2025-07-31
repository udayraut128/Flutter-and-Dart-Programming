## 🟩 **Topic 13: Libraries and Packages in Dart**

Libraries and packages are essential for **organizing code**, **reusing logic**, and **extending your app** using community-developed tools.

We'll break this into the following subtopics:

### ✅ 13.1: Importing Libraries

### ✅ 13.2: Creating Libraries

### ✅ 13.3: `pubspec.yaml`

### ✅ 13.4: Using External Packages

### ✅ 13.5: Custom Packages

---

### ✅ **13.1: Importing Libraries**

Dart supports different types of libraries:

* Built-in (core libraries like `dart:math`, `dart:io`)
* External (via `pub.dev`)
* Custom (your own Dart files/modules)

#### 🔹 Syntax:

```dart
import 'dart:math';        // Core library
import 'package:http/http.dart';  // External package
import 'my_library.dart';  // Custom local file
```

#### 🔹 Optional Aliases

```dart
import 'dart:math' as math;

void main() {
  print(math.sqrt(25));
}
```

#### 🔹 Selective Imports

```dart
import 'dart:math' show sqrt, pi; // Only import specific members
```

#### 🔹 Hiding Members

```dart
import 'dart:math' hide sin; // Import everything except sin
```

---

### ✅ **13.2: Creating Libraries**

You can create your own modular Dart libraries.

#### 🔹 `math_utils.dart`:

```dart
library math_utils;

int square(int x) => x * x;
int cube(int x) => x * x * x;
```

#### 🔹 Use it in `main.dart`:

```dart
import 'math_utils.dart';

void main() {
  print(square(4)); // Output: 16
}
```

---

### ✅ **13.3: `pubspec.yaml`**

This is the **configuration file** for your Dart or Flutter project.

It contains:

* Project metadata (name, version, description)
* Dependencies
* Assets
* Dev tools

#### 🔹 Example:

```yaml
name: my_app
description: A simple Dart project
version: 1.0.0

dependencies:
  http: ^0.14.0
```

Use this to install packages from [https://pub.dev](https://pub.dev)

---

### ✅ **13.4: Using External Packages**

You can install packages from **pub.dev**:

#### 🔹 Step-by-step:

1. Add dependency in `pubspec.yaml`:

```yaml
dependencies:
  http: ^0.14.0
```

2. Run:

```bash
dart pub get
```

3. Use in code:

```dart
import 'package:http/http.dart' as http;

void main() async {
  var response = await http.get(Uri.parse('https://example.com'));
  print(response.body);
}
```

---

### ✅ **13.5: Custom Packages**

You can create your own package to reuse across multiple projects.

#### 📁 Package Structure:

```
my_package/
├── lib/
│   └── my_package.dart
├── pubspec.yaml
```

Inside `my_package.dart`:

```dart
library my_package;

int add(int a, int b) => a + b;
```

Then in your main project:

```yaml
dependencies:
  my_package:
    path: ../my_package
```

---

### ✅ Summary

| Feature           | Purpose                                     |
| ----------------- | ------------------------------------------- |
| `import`          | Include libraries into your code            |
| `pubspec.yaml`    | Manage dependencies and settings            |
| External packages | Use community tools like `http`, `provider` |
| Custom libraries  | Reuse your own modular code                 |
| Custom packages   | Share libraries across multiple apps        |

---
 