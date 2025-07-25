### 📦 **Send Data to a New Screen in Flutter** – Detailed Guide

When developing apps, it’s common to **send data from one screen to another** — for example, passing a user ID, a name, or any other information. Flutter makes this very easy using constructors or named routes with arguments.

---

## 🔸 1. Basic Method: Using Constructor

This is the most common and simple way to pass data to another screen.

### ✅ Step-by-step Example

#### 🧱 First Screen (Sending Data)

```dart
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("First Screen")),
      body: Center(
        child: ElevatedButton(
          child: Text("Send Data"),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(
                builder: (context) => SecondScreen(message: "Hello from First!"),
              ),
            );
          },
        ),
      ),
    );
  }
}
```

#### 🧱 Second Screen (Receiving Data)

```dart
class SecondScreen extends StatelessWidget {
  final String message;

  SecondScreen({required this.message});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Second Screen")),
      body: Center(
        child: Text(
          message,
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

---

## 🔸 2. Using Named Routes with Arguments

This method is helpful in larger apps where navigation is handled with named routes.

### ✅ Step-by-step Example

#### Step 1️⃣: Define Routes in `MaterialApp`

```dart
void main() {
  runApp(MaterialApp(
    initialRoute: '/',
    routes: {
      '/': (context) => FirstScreen(),
      '/second': (context) => SecondScreen(),
    },
    onGenerateRoute: (settings) {
      if (settings.name == '/second') {
        final args = settings.arguments as ScreenArguments;
        return MaterialPageRoute(
          builder: (context) {
            return SecondScreenWithArgs(args: args);
          },
        );
      }
      return null;
    },
  ));
}
```

#### Step 2️⃣: First Screen – Sending Data

```dart
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("First Screen")),
      body: Center(
        child: ElevatedButton(
          child: Text("Send Data with Named Route"),
          onPressed: () {
            Navigator.pushNamed(
              context,
              '/second',
              arguments: ScreenArguments('Hello', 'This is the detail'),
            );
          },
        ),
      ),
    );
  }
}

class ScreenArguments {
  final String title;
  final String message;

  ScreenArguments(this.title, this.message);
}
```

#### Step 3️⃣: Second Screen – Receiving Data

```dart
class SecondScreenWithArgs extends StatelessWidget {
  final ScreenArguments args;

  SecondScreenWithArgs({required this.args});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text(args.title)),
      body: Center(
        child: Text(
          args.message,
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

---

## 🧠 Summary

| Method                      | Use Case                         |
| --------------------------- | -------------------------------- |
| Constructor Parameters      | Simple apps or limited screens   |
| Named Routes with Arguments | Large apps, decoupled navigation |

---

## ✅ Best Practices

* ✅ Use **constructors** when passing simple data.
* ✅ Use **route arguments** for scalable and modular code.
* ✅ Always validate and handle **null or wrong type** arguments.

---

