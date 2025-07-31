# 🌟 Flutter Navigation

---

## ✅ What is Navigation?

**Navigation** allows you to move between different screens (called **routes** or **pages**) in your app. Flutter manages navigation via a **stack of routes**, meaning you can push new pages on top or pop back to previous pages.

---

## 🔧 Core Concepts & Widgets

| Concept/Widget      | Description                                            |
| ------------------- | ------------------------------------------------------ |
| `Navigator`         | Manages a stack of routes; handles push/pop operations |
| `Route`             | A screen/page to navigate to                           |
| `MaterialPageRoute` | Common route that creates a material design page       |
| `push()`            | Pushes a new route on top of the stack                 |
| `pop()`             | Removes the top route, going back                      |
| `pushNamed()`       | Push route by name (requires route table setup)        |
| `popUntil()`        | Pops routes until a condition is met                   |
| `pushReplacement()` | Replace current route with a new one                   |

---

## 🧪 Example 1: Basic Navigation - Push & Pop

### First Screen (Home):

```dart
ElevatedButton(
  child: Text('Go to Second Screen'),
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => SecondScreen()),
    );
  },
)
```

### Second Screen:

```dart
Scaffold(
  appBar: AppBar(title: Text('Second Screen')),
  body: Center(
    child: ElevatedButton(
      child: Text('Go Back'),
      onPressed: () {
        Navigator.pop(context);
      },
    ),
  ),
)
```

---

## 🧪 Example 2: Passing Data Between Screens

### Pass data when navigating:

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailScreen(data: 'Hello from Home'),
  ),
);
```

### Receive data in new screen:

```dart
class DetailScreen extends StatelessWidget {
  final String data;
  DetailScreen({required this.data});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Details')),
      body: Center(child: Text(data)),
    );
  }
}
```

---

## 🧪 Example 3: Returning Data from a Screen

### Navigate and await result:

```dart
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SelectionScreen()),
);
print('Selected: $result');
```

### On SelectionScreen, return data:

```dart
ElevatedButton(
  onPressed: () {
    Navigator.pop(context, 'Option 1');
  },
  child: Text('Select Option 1'),
),
```

---

## 🧪 Example 4: Named Routes Navigation

### Define routes in `MaterialApp`:

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomeScreen(),
    '/second': (context) => SecondScreen(),
  },
);
```

### Navigate using named route:

```dart
Navigator.pushNamed(context, '/second');
```

### Pop is same:

```dart
Navigator.pop(context);
```

---

## 🧩 Bonus: Advanced Navigation

* **`pushReplacement()`** — Replaces current screen:

  ```dart
  Navigator.pushReplacement(
    context,
    MaterialPageRoute(builder: (context) => NewScreen()),
  );
  ```

* **`popUntil()`** — Pop multiple screens:

  ```dart
  Navigator.popUntil(context, ModalRoute.withName('/'));
  ```

* **Using `onGenerateRoute`** — Dynamically generate routes based on names and arguments.

---

## Summary Table

| Action             | Method                         | Purpose                           |
| ------------------ | ------------------------------ | --------------------------------- |
| Navigate to screen | `Navigator.push`               | Push new screen on stack          |
| Go back            | `Navigator.pop`                | Remove top screen                 |
| Navigate with data | Pass via constructor           | Send data to next screen          |
| Return data        | `Navigator.pop(context, data)` | Send data back to previous screen |
| Named routes       | `Navigator.pushNamed`          | Navigate using route names        |
| Replace screen     | `Navigator.pushReplacement`    | Replace current screen            |

---

# 🌐 Flutter Routing & Navigation in Detail

---

## 1. **MaterialPageRoute**

### ✅ What is MaterialPageRoute?

* A **MaterialPageRoute** is a simple way to define a route (screen) that transitions with Material Design animations.
* It creates a new page and adds it to the navigation stack.

### 🔧 How to use?

You create a new screen and navigate to it using:

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondScreen()),
);
```

---

### 🧪 Example 1: Simple MaterialPageRoute Navigation

```dart
// Home Screen Button
ElevatedButton(
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => SecondScreen()),
    );
  },
  child: Text('Go to Second Screen'),
);
```

---

### 🧪 Example 2: MaterialPageRoute with Data Passing

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailScreen(data: 'Hello, Flutter!'),
  ),
);
```

Inside `DetailScreen`:

```dart
class DetailScreen extends StatelessWidget {
  final String data;
  DetailScreen({required this.data});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Detail Screen")),
      body: Center(child: Text(data)),
    );
  }
}
```

---

## 2. **Named Routes**

### ✅ What are Named Routes?

* Named routes are strings mapped to WidgetBuilder functions.
* They make navigation easier to manage in larger apps by centralizing route definitions.

### 🔧 Setup in `MaterialApp`:

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomeScreen(),
    '/second': (context) => SecondScreen(),
    '/details': (context) => DetailScreen(),
  },
);
```

---

### 🧪 Example 3: Navigate using Named Routes

```dart
Navigator.pushNamed(context, '/second');
```

To pop:

```dart
Navigator.pop(context);
```

---

### 🧪 Example 4: Named Routes with Arguments

* When you want to pass data, you send arguments while navigating:

```dart
Navigator.pushNamed(
  context,
  '/details',
  arguments: 'Hello from Home',
);
```

* Then, in the receiving widget (`DetailScreen`), retrieve arguments:

```dart
@override
Widget build(BuildContext context) {
  final args = ModalRoute.of(context)!.settings.arguments as String;

  return Scaffold(
    appBar: AppBar(title: Text('Detail Screen')),
    body: Center(child: Text(args)),
  );
}
```

---

## 3. **RouteGenerator using `onGenerateRoute`**

### ✅ What is RouteGenerator?

* When your app needs **dynamic routing**, or to **handle unknown routes**, use a **RouteGenerator** function passed to `onGenerateRoute`.
* It centralizes route logic and argument parsing.

### 🔧 How to implement?

```dart
class RouteGenerator {
  static Route<dynamic> generateRoute(RouteSettings settings) {
    final args = settings.arguments;

    switch (settings.name) {
      case '/':
        return MaterialPageRoute(builder: (_) => HomeScreen());
      case '/details':
        if (args is String) {
          return MaterialPageRoute(
            builder: (_) => DetailScreen(data: args),
          );
        }
        return _errorRoute();
      default:
        return _errorRoute();
    }
  }

  static Route<dynamic> _errorRoute() {
    return MaterialPageRoute(
      builder: (_) => Scaffold(
        appBar: AppBar(title: Text('Error')),
        body: Center(child: Text('Route not found')),
      ),
    );
  }
}
```

### 🔧 Use it in MaterialApp:

```dart
MaterialApp(
  onGenerateRoute: RouteGenerator.generateRoute,
);
```

---

### 🧪 Example 5: Navigate with RouteGenerator

```dart
Navigator.pushNamed(
  context,
  '/details',
  arguments: 'Hello from RouteGenerator',
);
```

---

## 4. **Passing Data Between Screens**

### ✅ Ways to pass data:

* **Via Constructor** (when using `MaterialPageRoute`):

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailScreen(data: 'Passed Data'),
  ),
);
```

* **Via Named Routes Arguments**:

```dart
Navigator.pushNamed(
  context,
  '/details',
  arguments: 'Passed Data',
);
```

* **Returning Data Back** to previous screen:

```dart
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SelectionScreen()),
);

// Use the returned result
print('Selected: $result');
```

In `SelectionScreen`:

```dart
ElevatedButton(
  onPressed: () {
    Navigator.pop(context, 'Option 1');
  },
  child: Text('Choose Option 1'),
);
```

---

## Summary Table:

| Routing Method    | Usage                    | Data Passing Method                      | Example Method                                            |
| ----------------- | ------------------------ | ---------------------------------------- | --------------------------------------------------------- |
| MaterialPageRoute | Push via builder widget  | Constructor parameters                   | `MaterialPageRoute(builder: (context) => Screen(data))`   |
| Named Routes      | Push via route name      | Route arguments (`settings.arguments`)   | `Navigator.pushNamed(context, '/route', arguments: data)` |
| RouteGenerator    | Dynamic route generation | Arguments handled inside `generateRoute` | Custom `RouteGenerator.generateRoute` function            |
| Returning Data    | Pop with data            | `Navigator.pop(context, data)`           | Await `Navigator.push` to get result                      |

---

 
