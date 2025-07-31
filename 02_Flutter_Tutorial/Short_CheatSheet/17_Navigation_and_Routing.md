

---

# 🚀 Navigation and Routing in Flutter

Flutter provides powerful APIs for navigating between **screens (routes)** and passing data between them. There are multiple navigation approaches available, including:

* **Imperative (Navigator 1.0)** — classic push/pop method
* **Declarative (Navigator 2.0)** — state-driven, good for web and complex apps

---

## 📌 Terminology

| Term          | Meaning                                                              |
| ------------- | -------------------------------------------------------------------- |
| **Route**     | A screen/page/view in Flutter                                        |
| **Navigator** | A widget that manages a stack of routes (screens)                    |
| **Push**      | Navigate to a new screen (add it to the stack)                       |
| **Pop**       | Return to the previous screen (remove the top screen from the stack) |

---

## 🛣️ 1. Navigator 1.0 – Imperative Navigation (Beginner Friendly)

### 🔹 Push a new route

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondPage()),
);
```

### 🔹 Pop a route

```dart
Navigator.pop(context);
```

### 🔹 Pass data to a new route

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => SecondPage(message: 'Hello'),
  ),
);
```

### 🔹 Return data from a route

```dart
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondPage()),
);
print("Returned: $result");
```

In `SecondPage`:

```dart
Navigator.pop(context, 'Data to return');
```

---

## 🗺️ 2. Named Routes

Useful for larger apps with multiple screens.

### 🔹 Define Routes in `MaterialApp`

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomePage(),
    '/second': (context) => SecondPage(),
  },
)
```

### 🔹 Navigate using name

```dart
Navigator.pushNamed(context, '/second');
```

### 🔹 Pass arguments

```dart
Navigator.pushNamed(
  context,
  '/second',
  arguments: 'Hello from Home',
);
```

### 🔹 Retrieve arguments in second page

```dart
final args = ModalRoute.of(context)!.settings.arguments as String;
```

---

## 🔄 3. Replace Current Screen

Use this when you don’t want to return to the previous screen:

```dart
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => LoginPage()),
);
```

Or for named route:

```dart
Navigator.pushReplacementNamed(context, '/login');
```

---

## 🔄 4. Clear Stack and Go to New Route (Useful after login)

```dart
Navigator.pushAndRemoveUntil(
  context,
  MaterialPageRoute(builder: (context) => HomePage()),
  (Route<dynamic> route) => false,
);
```

---

## 🌐 5. Web/Advanced Navigation – Navigator 2.0 (Declarative)

Navigator 2.0 allows building apps with:

* Browser URL support
* Deep linking
* Declarative UI state management

Example packages using Navigator 2.0:

* [`go_router`](https://pub.dev/packages/go_router)
* [`beamer`](https://pub.dev/packages/beamer)
* [`auto_route`](https://pub.dev/packages/auto_route)

---

## 🧭 Using go\_router (Recommended for Complex Apps)

### 🔹 Add Dependency

```yaml
dependencies:
  go_router: ^14.1.0
```

### 🔹 Basic Setup

```dart
final GoRouter _router = GoRouter(
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => HomePage(),
    ),
    GoRoute(
      path: '/second',
      builder: (context, state) => SecondPage(),
    ),
  ],
);
```

### 🔹 Use in `MaterialApp.router`

```dart
MaterialApp.router(
  routerConfig: _router,
)
```

### 🔹 Navigate using go\_router

```dart
context.go('/second');
```

---

## 🧪 Summary Table

| Task                           | Code Example                               |
| ------------------------------ | ------------------------------------------ |
| Push new screen                | `Navigator.push(context, ...)`             |
| Pop current screen             | `Navigator.pop(context)`                   |
| Named route navigation         | `Navigator.pushNamed(context, '/route')`   |
| Pass data                      | `Navigator.pushNamed(..., arguments: ...)` |
| Replace current screen         | `Navigator.pushReplacement(...)`           |
| Clear back stack and push      | `Navigator.pushAndRemoveUntil(...)`        |
| Web URL & deep link navigation | `go_router`, `Navigator 2.0`               |

---

## 📝 Best Practices

* Use **named routes** or **go\_router** in medium/large apps.
* For small apps, simple `Navigator.push` is sufficient.
* Use **Navigator 2.0** (via go\_router or auto\_route) for web or deep linking.
* Handle route arguments and back navigation carefully.

---
 