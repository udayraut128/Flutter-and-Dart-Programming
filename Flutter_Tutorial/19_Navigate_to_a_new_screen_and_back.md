### 🔀 **Navigate to a New Screen and Back in Flutter** – Detailed Guide

In Flutter, navigation between screens (also called *routes*) is a key concept for building apps with multiple pages or views. Flutter provides a built-in `Navigator` widget and a `Route` system to manage navigation and screen history.

---

## 🧭 Overview

Flutter uses a **stack-based** navigation system:

* Each new screen is **pushed** onto the navigation stack.
* Going back **pops** the top screen off the stack.

---

## ✨ Basic Navigation Example

### Step 1️⃣: Create Two Screens

```dart
// main.dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Navigation Demo',
      home: FirstScreen(),
    );
  }
}
```

```dart
// First screen
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('First Screen')),
      body: Center(
        child: ElevatedButton(
          child: Text('Go to Second Screen'),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );
          },
        ),
      ),
    );
  }
}
```

```dart
// Second screen
class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Second Screen')),
      body: Center(
        child: ElevatedButton(
          child: Text('Go Back'),
          onPressed: () {
            Navigator.pop(context); // Pops SecondScreen and goes back
          },
        ),
      ),
    );
  }
}
```

---

## ⚙️ Explanation

### 🧱 `Navigator.push()`

* Adds (pushes) a new screen on top of the navigation stack.
* Syntax:

  ```dart
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => SecondScreen()),
  );
  ```

### 🧱 `Navigator.pop()`

* Removes (pops) the current screen off the stack, returning to the previous one.

---

## 🔁 Pass Data Between Screens

### 🔼 Passing Data *to* the Second Screen:

```dart
onPressed: () {
  Navigator.push(
    context,
    MaterialPageRoute(
      builder: (context) => SecondScreen(data: 'Hello from First Screen'),
    ),
  );
}
```

```dart
class SecondScreen extends StatelessWidget {
  final String data;
  SecondScreen({required this.data});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child: Text(data)),
    );
  }
}
```

---

### 🔽 Returning Data *from* the Second Screen:

```dart
// First Screen
onPressed: () async {
  final result = await Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => SecondScreen()),
  );
  print('Returned: $result');
}
```

```dart
// Second Screen
onPressed: () {
  Navigator.pop(context, 'This is returned!');
}
```

---

## 🗺️ Named Routes (Alternative)

Better for large apps with many screens.

### Define routes in `MaterialApp`:

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => FirstScreen(),
    '/second': (context) => SecondScreen(),
  },
);
```

### Navigate using route names:

```dart
Navigator.pushNamed(context, '/second');
Navigator.pop(context);
```

---

## 🧩 Custom Transitions (Optional)

```dart
Navigator.push(
  context,
  PageRouteBuilder(
    pageBuilder: (context, animation, secondaryAnimation) => SecondScreen(),
    transitionsBuilder: (context, animation, secondaryAnimation, child) {
      return FadeTransition(opacity: animation, child: child);
    },
  ),
);
```

---

## 🧠 Summary

| Action               | Code Example                              |
| -------------------- | ----------------------------------------- |
| Push screen          | `Navigator.push(...)`                     |
| Pop screen           | `Navigator.pop(context)`                  |
| Pass data to screen  | Pass via constructor                      |
| Get data from screen | `Navigator.pop(context, result)`          |
| Named routes         | `Navigator.pushNamed(context, '/second')` |
| Custom animation     | Use `PageRouteBuilder`                    |

---
 