## ✅ 1. Unit Testing

### 📌 What is Unit Testing?

Unit testing checks **individual functions, classes, or methods** to ensure they work correctly in isolation.

### 🛠 Tools Used:

* `test` package (built-in for Flutter)

---

### ✅ Basic Setup:

Add this to `dev_dependencies` in `pubspec.yaml`:

```yaml
dev_dependencies:
  test: ^1.21.0
```

Create test files inside `test/` folder:

```bash
test/
 └── utils_test.dart
```

---

### 🔍 Example 1: Testing a Calculator function

```dart
int add(int a, int b) => a + b;

void main() {
  test('adds two numbers', () {
    expect(add(2, 3), 5);
  });
}
```

---

### 🔍 Example 2: Testing a String Utility

```dart
bool isUpperCase(String s) => s == s.toUpperCase();

void main() {
  test('check if string is uppercase', () {
    expect(isUpperCase("HELLO"), true);
    expect(isUpperCase("Hello"), false);
  });
}
```

---

### 🔍 Example 3: Test Class Method

```dart
class BankAccount {
  double balance = 0;
  void deposit(double amount) => balance += amount;
}

void main() {
  test('deposit increases balance', () {
    final account = BankAccount();
    account.deposit(100);
    expect(account.balance, 100);
  });
}
```

---

## ✅ 2. Widget Testing

### 📌 What is Widget Testing?

Tests **UI components (widgets)** in isolation to ensure they behave as expected.

---

### 📦 Use:

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
```

---

### 🔍 Example 1: Test for `Text` Widget

```dart
void main() {
  testWidgets('MyText shows Hello', (WidgetTester tester) async {
    await tester.pumpWidget(MaterialApp(home: Text("Hello")));
    expect(find.text('Hello'), findsOneWidget);
  });
}
```

---

### 🔍 Example 2: Button Tap Changes Text

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  String text = "Before";
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text(text),
        ElevatedButton(
          onPressed: () => setState(() => text = "After"),
          child: Text("Tap"),
        )
      ],
    );
  }
}
```

**Test:**

```dart
testWidgets('tap changes text', (tester) async {
  await tester.pumpWidget(MaterialApp(home: MyWidget()));
  await tester.tap(find.byType(ElevatedButton));
  await tester.pump();
  expect(find.text("After"), findsOneWidget);
});
```

---

### 🔍 Example 3: Finding Widgets

```dart
expect(find.byType(TextField), findsOneWidget);
expect(find.widgetWithText(ElevatedButton, 'Submit'), findsOneWidget);
```

---

## ✅ 3. Integration Testing

### 📌 What is Integration Testing?

It tests the **complete app or a large portion**, simulating real user behavior (like typing, tapping).

---

### 📦 Packages Used:

* `integration_test`
* `flutter_test`

---

### 📄 Directory Structure:

```bash
integration_test/
 └── app_test.dart
```

**In `pubspec.yaml`:**

```yaml
dev_dependencies:
  integration_test:
    sdk: flutter
```

---

### 🔍 Example 1: Full App Test

```dart
void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets("Full flow test", (tester) async {
    app.main();
    await tester.pumpAndSettle();

    await tester.enterText(find.byType(TextField), 'Test');
    await tester.tap(find.byType(ElevatedButton));
    await tester.pump();

    expect(find.text("Welcome Test"), findsOneWidget);
  });
}
```

---

### 🔍 Example 2: Navigation Test

```dart
await tester.tap(find.text('Next Page'));
await tester.pumpAndSettle();
expect(find.text('This is Page 2'), findsOneWidget);
```

---

### 🔍 Example 3: Scroll and Find

```dart
await tester.fling(find.byType(ListView), Offset(0, -300), 1000);
await tester.pumpAndSettle();
expect(find.text("Item 30"), findsOneWidget);
```

---

## ✅ 4. `mockito` & `test` Packages

### 📌 What is `mockito`?

`mockito` is used to create **fake/mock classes** for dependencies like APIs, DBs, etc., during unit testing.

---

### 📦 Add dependencies:

```yaml
dev_dependencies:
  mockito: ^5.4.2
  test: ^1.21.0
  build_runner: ^2.4.6
```

---

### 🧪 Step-by-Step:

1. Create an abstract class or interface.
2. Use `@GenerateMocks()` to generate a mock.
3. Use it in your tests.

---

### 🧪 Example 1: Mock API service

```dart
abstract class ApiService {
  Future<String> fetchData();
}
```

Generate mock:

```dart
@GenerateMocks([ApiService])
void main() {}
```

Test:

```dart
final mockApi = MockApiService();

when(mockApi.fetchData()).thenAnswer((_) async => "Mock Data");

test('API returns mock data', () async {
  expect(await mockApi.fetchData(), "Mock Data");
});
```

---

### 🧪 Example 2: Mock Database

```dart
abstract class DbService {
  Future<void> insertUser(String name);
  Future<String> getUser();
}
```

Test with mock:

```dart
when(mockDb.insertUser("John")).thenAnswer((_) async => {});
when(mockDb.getUser()).thenAnswer((_) async => "John");

expect(await mockDb.getUser(), "John");
```

---

### 🧪 Example 3: Combine with Widget Test

You can mock backend and use it in widget testing:

```dart
await tester.pumpWidget(MyWidget(api: mockApi));
```

---

## ✅ Summary Table

| Type                | Purpose                       | Tools              | Example                     |
| ------------------- | ----------------------------- | ------------------ | --------------------------- |
| Unit Testing        | Test logic in isolation       | `test`             | Calculator, String checks   |
| Widget Testing      | Test UI components            | `flutter_test`     | Tap button, change text     |
| Integration Testing | Simulate full app usage       | `integration_test` | Full app interaction        |
| mockito             | Mock dependencies for testing | `mockito`, `test`  | Mock API, DB, Service calls |

---
 
