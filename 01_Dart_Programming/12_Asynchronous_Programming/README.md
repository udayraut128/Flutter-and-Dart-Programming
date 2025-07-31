## 🧠 What is Asynchronous Programming?

In Dart, **asynchronous programming** allows you to perform **long-running operations** (like network requests, file I/O, or database queries) **without blocking the main thread** (UI or event loop).

Instead of waiting for an operation to complete, the program continues and **responds later** when the operation finishes.

---

### 🟩 Subtopics under Asynchronous Programming:

1. **Futures**
2. **async and await**
3. **Streams**
4. **Stream Controllers**
5. **Stream Methods**
6. **await for**
7. **Error Handling in Async Code**

---

Let’s begin with the **first subtopic**:

---

## ✅ 12.1: **Futures in Dart**

### 🔹 What is a Future?

A **Future** represents a **value that will be available in the future**, after some delay.

It can be in one of three states:

* **Uncompleted**
* **Completed with data**
* **Completed with error**

---

### 🔹 Syntax

```dart
Future<String> fetchData() {
  return Future.delayed(Duration(seconds: 2), () {
    return "Data loaded";
  });
}
```

This simulates a delayed operation (like an API call).

---

### 🔹 Using then()

```dart
void main() {
  print("Start");

  fetchData().then((value) {
    print(value); // Output after 2 seconds: Data loaded
  });

  print("End");
}
```

**Output:**

```
Start
End
Data loaded
```

✅ The program doesn’t wait for `fetchData()` to finish. It moves to the next line and **executes the callback later** when data is ready.

---

### 🔹 Handling Errors

```dart
Future<String> fetchWithError() {
  return Future.delayed(Duration(seconds: 2), () {
    throw "Something went wrong!";
  });
}

void main() {
  fetchWithError()
    .then((value) => print(value))
    .catchError((error) => print("Caught error: $error"));
}
```

---

### 🔹 Chaining Futures

```dart
Future<int> add(int x, int y) {
  return Future.delayed(Duration(seconds: 1), () => x + y);
}

void main() {
  add(2, 3).then((sum) {
    print("Sum is $sum");
    return add(sum, 5);
  }).then((result) {
    print("New sum is $result");
  });
}
```

---

### 🔹 Future.value and Future.error

* `Future.value()` returns a value **immediately**.
* `Future.error()` returns an **immediate error**.

```dart
var future1 = Future.value("Immediate Value");
var future2 = Future.error("Immediate Error");
```

---

### Summary of `Future`:

| Feature            | Description                                |
| ------------------ | ------------------------------------------ |
| `Future.delayed()` | Simulates delayed operations               |
| `.then()`          | Executes when the Future completes         |
| `.catchError()`    | Handles errors thrown in the Future        |
| `Future.value()`   | Returns a Future with a value immediately  |
| `Future.error()`   | Returns a Future that completes with error |

---

## ✅ 12.2: `async` and `await` in Dart

---

### 🔹 Why use `async` and `await`?

While `.then()` and `.catchError()` work fine, they can **make code harder to read**, especially with nested operations. Dart provides `async` and `await` to write **asynchronous code that looks like synchronous code**.

---

### 🔹 Syntax Overview

* `async` is added to a function to mark it as **asynchronous**.
* `await` is used inside an `async` function to **pause execution until the awaited future completes**.

---

### 🔸 Example: Basic Usage

```dart
Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2));
  return "Data loaded";
}

void main() async {
  print("Start");

  String data = await fetchData();
  print(data);

  print("End");
}
```

**Output:**

```
Start
Data loaded
End
```

✅ The function `main()` is marked `async`, so it can use `await`. The program pauses at `await fetchData()` until the result is returned, then continues.

---

### 🔸 async Function Returning Future

```dart
Future<int> getNumber() async {
  return 42; // Automatically wrapped in Future
}
```

---

### 🔸 Combining Multiple Awaits

```dart
Future<void> multipleTasks() async {
  String task1 = await Future.delayed(Duration(seconds: 1), () => "First");
  String task2 = await Future.delayed(Duration(seconds: 1), () => "Second");
  print("$task1 then $task2");
}
```

---

### 🔸 Handling Errors with try-catch

You can use standard `try-catch` blocks with `await`.

```dart
Future<void> getData() async {
  try {
    String data = await Future.delayed(Duration(seconds: 2), () {
      throw "Failed to load data";
    });
    print(data);
  } catch (e) {
    print("Caught error: $e");
  }
}
```

---

### 🔸 async in Anonymous Functions

```dart
void main() {
  Future(() async {
    await Future.delayed(Duration(seconds: 1));
    print("Async in anonymous function");
  });
}
```

---

### 🔸 Limitations

* `await` **can only be used inside async functions**.
* An `async` function **always returns a Future**, even if you return a value directly.

```dart
Future<String> foo() async {
  return "bar"; // this is Future<String>
}
```

---

### Summary Table

| Keyword     | Purpose                                         |
| ----------- | ----------------------------------------------- |
| `async`     | Marks a function as asynchronous                |
| `await`     | Waits for a Future to complete before moving on |
| `try-catch` | Handles exceptions in `async` functions         |

---
 
## ✅ **12.3: Streams in Dart**

---

### 🔹 What is a Stream?

A **Stream** is a sequence of asynchronous events. It's used when:

* You expect **multiple values over time** (not just one).
* Example: user keystrokes, sensor values, live data, socket communication, etc.

Think of a **Future** as a **single value in the future**, and a **Stream** as **many values over time**.

---

### 🔸 Stream Types

1. **Single-subscription Stream**

   * Only one listener can listen at a time.
   * Example: HTTP response.

2. **Broadcast Stream**

   * Multiple listeners can listen.
   * Example: UI events, WebSocket data.

---

### 🔹 Basic Example – Single-Subscription Stream

```dart
Stream<int> countStream() async* {
  for (int i = 1; i <= 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i; // Yield sends the value
  }
}

void main() async {
  await for (int value in countStream()) {
    print("Value: $value");
  }
}
```

**Output:**

```
Value: 1
Value: 2
Value: 3
Value: 4
Value: 5
```

---

### 🔹 Listening to Streams Using `.listen()`

```dart
Stream<String> getNames() async* {
  yield "Alice";
  yield "Bob";
  yield "Charlie";
}

void main() {
  getNames().listen((name) {
    print("Received: $name");
  });
}
```

---

### 🔹 Broadcast Stream Example

```dart
Stream<int> getNumbers() {
  return Stream<int>.periodic(Duration(seconds: 1), (x) => x).take(3);
}

void main() {
  var stream = getNumbers().asBroadcastStream();

  stream.listen((val) => print("Listener 1: $val"));
  stream.listen((val) => print("Listener 2: $val"));
}
```

---

### 🔹 Stream Transformation

You can use `.map()`, `.where()`, `.take()` etc. like lists:

```dart
getNumbers()
  .where((num) => num % 2 == 0)
  .listen((val) => print("Even: $val"));
```

---

### 🔹 Error Handling in Streams

```dart
Stream<int> faultyStream() async* {
  yield 1;
  throw Exception("Stream error");
  yield 2;
}

void main() {
  faultyStream().listen(
    (val) => print("Received: $val"),
    onError: (err) => print("Error: $err"),
    onDone: () => print("Stream closed"),
  );
}
```

---

### 🔹 Summary

| Concept               | Description                              |
| --------------------- | ---------------------------------------- |
| `Stream`              | Emits multiple async values over time    |
| `await for`           | Used to loop over stream values          |
| `.listen()`           | Attach listener to stream                |
| `yield`               | Emits a value from an `async*` generator |
| `asBroadcastStream()` | Allows multiple listeners                |

---

## ✅ **12.4: Stream Controllers in Dart**

---

### 🔹 What is a StreamController?

A **StreamController** is used to **create and manage a custom Stream manually**.

It gives you:

* A `stream` to **listen to**
* A `sink` to **add data, errors, or close the stream**

---

### 🔸 Creating a StreamController

```dart
import 'dart:async';

void main() {
  final controller = StreamController<String>();

  // Listening to the stream
  controller.stream.listen(
    (data) => print('Data received: $data'),
    onError: (err) => print('Error: $err'),
    onDone: () => print('Stream closed'),
  );

  // Adding data to the stream
  controller.sink.add('Hello');
  controller.sink.add('World');

  // Adding an error
  controller.sink.addError('Oops! Something went wrong.');

  // Closing the stream
  controller.close();
}
```

---

### 🔹 Explanation

| Part                              | Meaning                                     |
| --------------------------------- | ------------------------------------------- |
| `controller.stream`               | The stream to which listeners can subscribe |
| `controller.sink.add(value)`      | Adds data to stream                         |
| `controller.sink.addError(error)` | Sends error to stream                       |
| `controller.close()`              | Closes the stream                           |

---

### 🔹 Broadcast StreamController

If you want **multiple listeners**, convert it to a broadcast controller:

```dart
final controller = StreamController<String>.broadcast();

controller.stream.listen((data) => print('Listener 1: $data'));
controller.stream.listen((data) => print('Listener 2: $data'));

controller.sink.add("Welcome!");
```

---

### 🔹 Common Use Cases

* Real-time user input (e.g., search fields)
* Event buses
* Custom business logic streams

---

### ⚠️ Important

* Always call `close()` when done — failing to do so causes memory leaks.
* Don’t add to the stream after closing it — it throws an error.

---

### 🔹 Example: Real-time Counter

```dart
final counterController = StreamController<int>();
int count = 0;

void main() {
  counterController.stream.listen((val) => print("Count: $val"));

  // Simulate a counter
  Timer.periodic(Duration(seconds: 1), (timer) {
    counterController.sink.add(++count);
    if (count == 5) {
      counterController.close();
      timer.cancel();
    }
  });
}
```

---

## ✅ **12.5: Stream Methods in Dart**

---

Dart provides many **built-in methods** on streams that allow you to **transform, filter, combine, and handle** data easily — similar to how list methods work, but for asynchronous data.

---

### 🔹 Common Stream Methods

| Method          | Description                                       |
| --------------- | ------------------------------------------------- |
| `listen()`      | Subscribes to the stream                          |
| `map()`         | Transforms each event                             |
| `where()`       | Filters events based on condition                 |
| `take(n)`       | Takes only the first `n` events                   |
| `skip(n)`       | Skips the first `n` events                        |
| `first`, `last` | Gets first or last element from the stream        |
| `reduce()`      | Reduces elements into a single value              |
| `toList()`      | Collects stream into a List                       |
| `forEach()`     | Performs an action for each element               |
| `handleError()` | Handles errors emitted from the stream            |
| `timeout()`     | Throws error if events don't arrive in given time |

---

### 🔸 Example 1: `map()` and `where()`

```dart
Stream<int> numberStream() async* {
  for (int i = 1; i <= 5; i++) {
    yield i;
  }
}

void main() {
  numberStream()
      .where((x) => x % 2 == 0)   // Only even numbers
      .map((x) => x * x)          // Square the number
      .listen((val) => print("Value: $val"));
}
```

**Output:**

```
Value: 4
Value: 16
```

---

### 🔸 Example 2: `take()` and `skip()`

```dart
void main() {
  numberStream()
      .skip(2)      // Skip first 2: 1, 2
      .take(2)      // Take next 2: 3, 4
      .listen((val) => print("Stream: $val"));
}
```

**Output:**

```
Stream: 3
Stream: 4
```

---

### 🔸 Example 3: `reduce()`

```dart
void main() async {
  final sum = await numberStream().reduce((a, b) => a + b);
  print("Sum: $sum");
}
```

**Output:**

```
Sum: 15
```

---

### 🔸 Example 4: `toList()` and `forEach()`

```dart
void main() async {
  List<int> list = await numberStream().toList();
  print("List: $list");

  await numberStream().forEach((e) => print("Item: $e"));
}
```

---

### 🔸 Example 5: `handleError()` and `timeout()`

```dart
Stream<int> faultyStream() async* {
  yield 1;
  throw Exception("Something went wrong");
  yield 2;
}

void main() {
  faultyStream().listen(
    (val) => print("Value: $val"),
    onError: (err) => print("Error caught: $err"),
    onDone: () => print("Done"),
  );
}
```

---

### 🔹 Summary Table

| Method          | Purpose              |
| --------------- | -------------------- |
| `map()`         | Change data values   |
| `where()`       | Filter values        |
| `take(n)`       | Take first n items   |
| `skip(n)`       | Skip first n items   |
| `reduce()`      | Combine all values   |
| `toList()`      | Convert to list      |
| `handleError()` | Handle stream errors |

---
 

## ✅ **12.6: `await for` in Dart**

---

### 🔷 What is `await for`?

The `await for` loop is used to **asynchronously iterate over a `Stream`** in Dart.

It's similar to a regular `for` loop, but it waits for **each event** from the stream **before continuing**. It only works inside an `async` function.

---

### 🔹 Syntax:

```dart
await for (var element in stream) {
  // process element
}
```

> ⚠️ Must be used in an `async` function marked with `async`.

---

### 🔸 Example 1: Basic `await for` usage

```dart
Stream<int> numberStream() async* {
  for (int i = 1; i <= 3; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}

Future<void> main() async {
  await for (var value in numberStream()) {
    print("Received: $value");
  }
  print("Stream completed.");
}
```

**Output:**

```
Received: 1
Received: 2
Received: 3
Stream completed.
```

✅ Here, Dart waits for each number from the stream before moving on.

---

### 🔸 Example 2: Using `await for` with a condition

```dart
Stream<String> wordStream() async* {
  yield "Dart";
  yield "is";
  yield "awesome";
}

Future<void> main() async {
  await for (var word in wordStream()) {
    if (word == "awesome") break;
    print("Word: $word");
  }
}
```

**Output:**

```
Word: Dart
Word: is
```

---

### 🔹 Key Points

| Feature           | Description                                      |
| ----------------- | ------------------------------------------------ |
| `await for`       | Waits for each stream event                      |
| Only for `Stream` | Cannot be used with `Future`                     |
| Needs `async`     | Only allowed inside `async` functions            |
| Cancels on error  | Stops if stream throws an error (unless handled) |

---

### 🔸 Handling Errors

```dart
Stream<int> errorStream() async* {
  yield 1;
  throw Exception("Oops!");
  yield 2;
}

Future<void> main() async {
  try {
    await for (var val in errorStream()) {
      print(val);
    }
  } catch (e) {
    print("Caught error: $e");
  }
}
```

**Output:**

```
1
Caught error: Exception: Oops!
```

---

### 🔹 Summary

* `await for` is the best way to **consume streams sequentially**.
* It simplifies stream handling without needing `.listen()` or callbacks.
* Wrap in `try-catch` to handle errors gracefully.

---

## ✅ **12.7: Error Handling in Async Code**

---

### ⚠️ Why is Error Handling Important?

When dealing with **Futures** or **Streams**, errors can occur due to:

* Network failures
* File access issues
* Programming bugs
* Unhandled exceptions in asynchronous callbacks

If not handled, they can **crash your app**.

---

### 🔹 1. Handling Errors in Futures

#### ✅ Example with `.catchError()`

```dart
Future<int> getNumber() {
  return Future.delayed(Duration(seconds: 1), () {
    throw Exception("Something went wrong");
  });
}

void main() {
  getNumber()
      .then((value) => print("Value: $value"))
      .catchError((error) => print("Caught error: $error"));
}
```

---

#### ✅ Using `try-catch` with `async-await`

```dart
Future<int> getValue() async {
  throw Exception("Error occurred");
}

Future<void> main() async {
  try {
    var value = await getValue();
    print("Value: $value");
  } catch (e) {
    print("Caught error: $e");
  }
}
```

---

### 🔹 2. Handling Errors in Streams

#### ✅ Using `onError` with `.listen()`

```dart
Stream<int> numberStream() async* {
  yield 1;
  throw Exception("Stream error");
  yield 2;
}

void main() {
  numberStream().listen(
    (data) => print("Data: $data"),
    onError: (err) => print("Caught stream error: $err"),
    onDone: () => print("Stream closed"),
  );
}
```

---

#### ✅ Using `try-catch` with `await for`

```dart
Stream<String> words() async* {
  yield "Hello";
  throw Exception("Oops!");
}

Future<void> main() async {
  try {
    await for (var word in words()) {
      print("Word: $word");
    }
  } catch (e) {
    print("Caught error: $e");
  }
}
```

---

### 🧠 Best Practices

| Tip                                | Description                               |
| ---------------------------------- | ----------------------------------------- |
| ✅ Always use `try-catch`           | Protect your `async` and `await` calls    |
| ✅ Use `.catchError()` with Futures | When using `then()`, attach error handler |
| ✅ Handle stream errors in `listen` | Use `onError` to catch stream exceptions  |
| ✅ Don't ignore errors              | Silently failing code is hard to debug    |

---

### 🟨 Advanced: `rethrow`

Sometimes you want to catch an error, log it, and **rethrow it**:

```dart
Future<void> risky() async {
  try {
    throw Exception("Network issue");
  } catch (e) {
    print("Logging: $e");
    rethrow;
  }
}
```

---

### ✅ Summary

* Use `try-catch` with `await` and `await for`
* Use `.catchError()` when chaining with `then()`
* Handle all potential failure points — async code can fail at any time
* Use `onError` for Streams, and always consider `onDone` too

---

🟢 That completes **Asynchronous Programming in Dart** (Topic 12).

---
 
