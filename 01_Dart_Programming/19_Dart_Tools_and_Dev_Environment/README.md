## 🟩 **Topic 19: Dart Tools & Dev Environment**

This section covers **essential Dart command-line tools** and utilities that improve development, formatting, analysis, and deployment.

---

### 🔹 19.1: `dartfmt` – Dart Code Formatter

* **Purpose**: Automatically formats your Dart code to make it readable and consistent.
* **Command**:

  ```bash
  dart format lib/
  ```
* It works on:

  * `.dart` files
  * Entire directories (`lib/`, `test/`, etc.)
* **Before**:

  ```dart
  void main(){print("Hello");}
  ```
* **After formatting**:

  ```dart
  void main() {
    print("Hello");
  }
  ```

---

### 🔹 19.2: `dart analyze` – Static Analyzer

* **Purpose**: Checks your Dart code for errors, style issues, and potential bugs.
* **Command**:

  ```bash
  dart analyze
  ```
* **Output**: Shows warnings, errors, and hints with file and line number.

Example Output:

```
lib/main.dart:5:14: Warning: The value of the local variable 'name' isn't used.
```

---

### 🔹 19.3: `dartdoc` – Documentation Generator

* **Purpose**: Generates documentation from Dart code comments (like Javadoc or Doxygen).
* **Command**:

  ```bash
  dart doc
  ```
* **Generates**: HTML docs in a `doc/api` folder.

> You must use Dart-style comments (`///`) for it to pick up on documentation.

Example:

```dart
/// Adds two numbers.
int add(int a, int b) => a + b;
```

---

### 🔹 19.4: `pub` Tool

* **Purpose**: Manages Dart packages and dependencies via `pubspec.yaml`.

* **Common Commands**:

  ```bash
  dart pub get        # Fetch packages
  dart pub upgrade    # Upgrade packages
  dart pub outdated   # Show outdated packages
  ```

* Run it whenever you change `pubspec.yaml`.

---

### 🔹 19.5: `dart compile`

* **Purpose**: Compiles Dart code to native machine code, JavaScript, or kernel bytecode.
* **Commands**:

  * Native executable:

    ```bash
    dart compile exe bin/main.dart
    ```
  * Web (JavaScript):

    ```bash
    dart compile js bin/main.dart -o out.js
    ```

---

### 🔹 19.6: `dart run`

* **Purpose**: Runs a Dart script or entry point in your project.
* **Command**:

  ```bash
  dart run
  ```
* Automatically compiles and runs the main file or specified `.dart` file.

Example:

```bash
dart run bin/my_script.dart
```

---

## 🧠 Summary Table

| Tool         | Purpose                     | Example Command              |
| ------------ | --------------------------- | ---------------------------- |
| dartfmt      | Formats Dart code           | `dart format lib/`           |
| dartanalyzer | Finds errors & warnings     | `dart analyze`               |
| dartdoc      | Generates API docs          | `dart doc`                   |
| pub          | Manages dependencies        | `dart pub get`               |
| dart compile | Compile to executable or JS | `dart compile exe file.dart` |
| dart run     | Run Dart app or file        | `dart run bin/app.dart`      |

---

 
