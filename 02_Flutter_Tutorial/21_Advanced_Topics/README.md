## 🔹 1. Isolates & Concurrency

### 🔸 What is an Isolate?

Dart is **single-threaded**, but isolates allow **parallel execution** without shared memory (like threads in other languages).

### 🔹 Use Cases:

* Heavy computations
* Background processing
* File parsing
* Network operations (in background)

---

### 🔍 Example 1: Using `compute()` function

```dart
import 'package:flutter/foundation.dart';

int heavyTask(int num) {
  return num * num;
}

void main() async {
  final result = await compute(heavyTask, 20);
  print(result); // 400
}
```

---

### 🔍 Example 2: Manual Isolate

```dart
import 'dart:isolate';

void isolateEntry(SendPort sendPort) {
  sendPort.send('Hello from isolate');
}

void main() async {
  final receivePort = ReceivePort();
  await Isolate.spawn(isolateEntry, receivePort.sendPort);

  receivePort.listen((message) {
    print(message); // Hello from isolate
  });
}
```

---

### 🔍 Example 3: Isolate for file I/O

* Parse JSON in isolate to avoid UI freeze

```dart
parseInBackground(String data) {
  return jsonDecode(data);
}
```

---

### 🔍 Example 4: Using isolates with `ReceivePort` and `SendPort` to perform secure communication.

---

## 🔹 2. Streams & BLoC Pattern

### 🔸 Streams:

* Asynchronous data pipelines (e.g., Firebase, sensors, APIs)
* Can be single or broadcast streams

### 🔸 BLoC (Business Logic Component):

* Separates UI from logic
* Uses `Streams` and `Sinks` for communication

---

### 🔍 Example 1: Simple Stream

```dart
Stream<int> numberStream() async* {
  for (int i = 0; i < 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}
```

---

### 🔍 Example 2: StreamBuilder

```dart
StreamBuilder(
  stream: numberStream(),
  builder: (context, snapshot) {
    if (snapshot.hasData) return Text('${snapshot.data}');
    return CircularProgressIndicator();
  },
)
```

---

### 🔍 Example 3: Simple BLoC

```dart
class CounterBloc {
  final _counter = StreamController<int>();
  int _count = 0;

  Stream<int> get stream => _counter.stream;
  void increment() {
    _count++;
    _counter.sink.add(_count);
  }

  void dispose() {
    _counter.close();
  }
}
```

---

### 🔍 Example 4: Using `flutter_bloc` package

```dart
BlocProvider(
  create: (_) => CounterCubit(),
  child: CounterScreen(),
)
```

---

## 🔹 3. Flutter Web Specifics

### 🔸 Key Concepts:

* Responsive design
* Routing via `go_router` or `Navigator`
* Web hosting and caching
* Browser APIs (e.g., localStorage)

---

### 🔍 Example 1: Responsive Layout

```dart
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 600) return DesktopLayout();
    else return MobileLayout();
  },
)
```

---

### 🔍 Example 2: Named Routing in Web

```dart
MaterialApp(
  routes: {
    '/': (context) => Home(),
    '/about': (context) => AboutPage(),
  },
)
```

URL bar updates accordingly.

---

### 🔍 Example 3: Hosting on GitHub Pages

```bash
flutter build web
```

Push `build/web/` to `gh-pages` branch.

---

### 🔍 Example 4: Using `url_launcher` in web

```dart
launch("https://flutter.dev");
```

---

## 🔹 4. CustomPaint & Canvas

### 🔸 What is CustomPaint?

* Widget used to draw directly on the screen using Canvas (shapes, lines, graphs, charts)

---

### 🔍 Example 1: Drawing Circle

```dart
class MyPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()..color = Colors.blue;
    canvas.drawCircle(Offset(size.width / 2, size.height / 2), 40, paint);
  }

  @override
  bool shouldRepaint(_) => false;
}
```

---

### 🔍 Example 2: Drawing Lines

```dart
canvas.drawLine(
  Offset(0, 0),
  Offset(100, 100),
  Paint()
    ..color = Colors.red
    ..strokeWidth = 2,
);
```

---

### 🔍 Example 3: Drawing Text

```dart
TextPainter(
  text: TextSpan(text: 'Hello', style: TextStyle(color: Colors.black)),
  textDirection: TextDirection.ltr,
)..layout()
  ..paint(canvas, Offset(0, 0));
```

---

### 🔍 Example 4: Drawing Rectangles

```dart
canvas.drawRect(
  Rect.fromLTWH(10, 10, 100, 50),
  Paint()..color = Colors.green,
);
```

---

## 🔹 5. Flutter DevTools

### 🔸 DevTools Features:

* Widget Inspector
* Timeline for performance
* Memory usage monitor
* Network calls and logs
* CPU profiler

---

### 🔍 Example 1: Launching DevTools

```bash
flutter pub global activate devtools
flutter pub global run devtools
```

Or run:

```bash
flutter run --debug
```

And open: [http://127.0.0.1:9100](http://127.0.0.1:9100)

---

### 🔍 Example 2: Debugging Widget Tree

Use **Widget Inspector** to explore layout, padding, and margins.

---

### 🔍 Example 3: Timeline View

View how long each frame takes, and identify jank sources.

---

### 🔍 Example 4: Memory Leaks

Track allocations and garbage collection to debug memory leaks.

---

## 🔹 6. Performance Optimization

### 🔸 Common Issues:

* Overbuilding widgets
* Large widget trees
* Too many rebuilds
* Unoptimized images/assets

---

### 🔍 Example 1: Use `const` Widgets

```dart
const Text('Hello');
```

Reduces rebuild overhead.

---

### 🔍 Example 2: Use `RepaintBoundary`

```dart
RepaintBoundary(
  child: MyCustomWidget(),
)
```

Prevents unnecessary repainting.

---

### 🔍 Example 3: Use `ListView.builder` for long lists

```dart
ListView.builder(
  itemCount: 10000,
  itemBuilder: (_, i) => Text('Item $i'),
)
```

---

### 🔍 Example 4: Minify and Compress Assets

* Use `.webp` instead of `.png`
* Compress large images
* Lazy load heavy widgets

---

## ✅ Summary Table

| Topic              | Use Cases             | Examples                                       |
| ------------------ | --------------------- | ---------------------------------------------- |
| Isolates           | Parallel computation  | `compute()`, `Isolate.spawn()`                 |
| Streams & BLoC     | Reactive data flow    | `StreamController`, `BlocBuilder`              |
| Flutter Web        | Web builds & routing  | `LayoutBuilder`, `MaterialApp routes`          |
| CustomPaint/Canvas | Custom UI drawings    | `drawLine()`, `drawCircle()`                   |
| DevTools           | Debugging & profiling | Widget Inspector, Memory tab                   |
| Performance        | Optimizing UI & logic | `const`, `RepaintBoundary`, `ListView.builder` |

---

 
