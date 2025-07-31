## 🟪 **Topic 18: Isolates and Concurrency in Dart**

---

### 📌 What is an Isolate?

In Dart, **Isolates** are the **units of concurrency**.
Each Isolate runs in its **own memory space**, **independently**, and **does not share memory** with other isolates.

> Dart **does not use threads** like Java or C++. Instead, it uses **Isolates** to perform parallel computations.

---

### ✅ Why Use Isolates?

* To run **CPU-intensive** or **long-running** tasks **without blocking** the main thread (UI in Flutter).
* Ideal for **image processing**, **file parsing**, **networking**, etc.
* Avoids race conditions as **data is not shared**, but passed via **messages**.

---

## 🔹 18.1: Basic Concepts

| Concept          | Meaning                  |
| ---------------- | ------------------------ |
| `Isolate`        | Independent Dart process |
| `spawn()`        | Creates a new isolate    |
| `SendPort`       | Used to send messages    |
| `ReceivePort`    | Used to receive messages |
| `Isolate.exit()` | Terminates an isolate    |

---

## 🔹 18.2: Example – Basic Isolate Communication

```dart
import 'dart:isolate';

void entryPoint(SendPort sendPort) {
  sendPort.send("Hello from Isolate!");
}

void main() async {
  ReceivePort receivePort = ReceivePort();

  await Isolate.spawn(entryPoint, receivePort.sendPort);

  receivePort.listen((message) {
    print("Main Isolate received: $message");
    receivePort.close();
  });
}
```

🟢 Output:
`Main Isolate received: Hello from Isolate!`

---

## 🔹 18.3: Two-Way Communication Example

```dart
import 'dart:isolate';

void isolateFunction(SendPort mainSendPort) {
  ReceivePort isolateReceivePort = ReceivePort();
  mainSendPort.send(isolateReceivePort.sendPort);

  isolateReceivePort.listen((message) {
    print("Isolate received: $message");
    isolateReceivePort.close();
  });
}

void main() async {
  ReceivePort mainReceivePort = ReceivePort();

  await Isolate.spawn(isolateFunction, mainReceivePort.sendPort);

  SendPort? isolateSendPort;

  mainReceivePort.listen((message) {
    if (message is SendPort) {
      isolateSendPort = message;
      isolateSendPort?.send("Hello Isolate!");
    }
  });
}
```

🟢 Output:

```
Isolate received: Hello Isolate!
```

---

## 🔹 18.4: Long-running Task Example

```dart
void heavyComputation(SendPort sendPort) {
  int result = 0;
  for (int i = 0; i < 1000000000; i++) {
    result += i;
  }
  sendPort.send(result);
}
```

Use it with `Isolate.spawn()` so it doesn’t block the UI.

---

## 🧠 Key Takeaways

| Feature       | Dart Isolates                              |
| ------------- | ------------------------------------------ |
| Shared Memory | ❌ No (data copied via messages)            |
| Lightweight   | ✅ Yes, like lightweight processes          |
| Communication | ✅ Through `SendPort` and `ReceivePort`     |
| Use Case      | Long-running tasks, background computation |

---

### 🔥 Bonus: In Flutter

Use **`compute()`** for simple isolate usage:

```dart
import 'package:flutter/foundation.dart';

int longTask(int n) {
  return n * 2;
}

void main() async {
  int result = await compute(longTask, 10);
  print(result); // 20
}
```

---

