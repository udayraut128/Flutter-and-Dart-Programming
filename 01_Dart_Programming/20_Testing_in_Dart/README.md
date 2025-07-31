## 🟦 **Topic 20: Testing in Dart**

Testing is crucial to ensure your code is **correct**, **reliable**, and **maintainable**. Dart offers strong testing support, especially when building Flutter or command-line apps.

We’ll break this down into 5 subtopics:

---

### 🔹 20.1: **Unit Testing**

**Unit tests** check individual functions, classes, or methods in isolation.

#### ✅ Getting Started

1. Add the test package to your `pubspec.yaml`:

   ```yaml
   dev_dependencies:
     test: ^1.24.0
   ```

2. Create a test file in `test/` directory:

   ```dart
   // test/calculator_test.dart
   import 'package:test/test.dart';
   import '../lib/calculator.dart';

   void main() {
     test('adds two numbers', () {
       expect(add(2, 3), 5);
     });
   }
   ```

3. Run the test:

   ```bash
   dart test
   ```

#### ✅ Output

```
✓ adds two numbers
All tests passed!
```

---

### 🔹 20.2: **Widget Testing (Flutter)**

Used for testing **Flutter widgets** by simulating UI behavior.

#### Example:

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:myapp/main.dart';

void main() {
  testWidgets('Counter increments smoke test', (WidgetTester tester) async {
    await tester.pumpWidget(MyApp());

    expect(find.text('0'), findsOneWidget);
    await tester.tap(find.byIcon(Icons.add));
    await tester.pump();
    expect(find.text('1'), findsOneWidget);
  });
}
```

> Use `flutter test` instead of `dart test` for widget testing.

---

### 🔹 20.3: **Integration Testing**

Tests the full app flow from start to finish — often involving UI, backend, databases, etc.

#### Setup (Flutter):

1. Add dependency in `pubspec.yaml`:

   ```yaml
   integration_test:
   ```

2. Create test:

   ```dart
   import 'package:flutter_test/flutter_test.dart';
   import 'package:integration_test/integration_test.dart';
   import 'package:myapp/main.dart';

   void main() {
     IntegrationTestWidgetsFlutterBinding.ensureInitialized();

     testWidgets('full app test', (tester) async {
       await tester.pumpWidget(MyApp());
       // simulate taps and expect full-flow
     });
   }
   ```

3. Run the test:

   ```bash
   flutter test integration_test/app_test.dart
   ```

---

### 🔹 20.4: **Using `test` Package**

The `test` package provides:

* `test()` blocks
* Matchers like `expect()`
* `setUp()` / `tearDown()` for preparation
* Grouping with `group()`

#### Example:

```dart
void main() {
  group('Math Utils', () {
    test('square of 3 is 9', () {
      expect(square(3), equals(9));
    });

    test('square of 0 is 0', () {
      expect(square(0), equals(0));
    });
  });
}
```

---

### 🔹 20.5: **Mocking**

Used to simulate behavior of classes like APIs or databases.

#### Add mocktail or mockito to `pubspec.yaml`:

```yaml
dev_dependencies:
  mockito: ^5.4.0
  build_runner: ^2.4.0
```

#### Example using `mockito`:

```dart
class MockService extends Mock implements ApiService {}

void main() {
  final mock = MockService();

  when(() => mock.fetchData()).thenReturn('Mocked Response');

  test('fetches data', () {
    expect(mock.fetchData(), 'Mocked Response');
  });
}
```

---

## 🧠 Summary

| Type             | Description                              | Command        |
| ---------------- | ---------------------------------------- | -------------- |
| Unit Test        | Test individual functions or classes     | `dart test`    |
| Widget Test      | Test Flutter UI widgets                  | `flutter test` |
| Integration Test | Full app flow testing                    | `flutter test` |
| Mocking          | Simulate APIs/DBs using mockito/mocktail | Uses `mockito` |

---
 