### 🧭 Add a Drawer to a Screen in Flutter – Full Detailed Guide

A **Drawer** in Flutter is a slide-in navigation panel that typically appears from the **left side** of the screen. It’s commonly used in apps to provide **navigation options**, **user profiles**, **settings**, etc.

---

## 📌 Overview

* A **Drawer** is added to a `Scaffold` using the `drawer:` parameter.
* The drawer typically contains a `ListView` of `ListTile`s.
* A **hamburger icon** is automatically provided by Flutter when a drawer is attached to a `Scaffold`.

---

## 🧱 Basic Example

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Drawer Example'),
      ),
      drawer: Drawer(
        child: ListView(
          padding: EdgeInsets.zero,
          children: [
            // Optional: User Account Header
            DrawerHeader(
              decoration: BoxDecoration(
                color: Colors.blue,
              ),
              child: Text(
                'Welcome User!',
                style: TextStyle(color: Colors.white, fontSize: 24),
              ),
            ),

            // Navigation items
            ListTile(
              leading: Icon(Icons.home),
              title: Text('Home'),
              onTap: () {
                Navigator.pop(context); // Closes the drawer
              },
            ),
            ListTile(
              leading: Icon(Icons.settings),
              title: Text('Settings'),
              onTap: () {
                Navigator.pop(context);
              },
            ),
            ListTile(
              leading: Icon(Icons.logout),
              title: Text('Logout'),
              onTap: () {
                Navigator.pop(context);
              },
            ),
          ],
        ),
      ),
      body: Center(
        child: Text('Main Screen Content'),
      ),
    );
  }
}
```

---

## 🔍 Drawer Key Components

| Component         | Description                                 |
| ----------------- | ------------------------------------------- |
| `drawer:`         | Property of `Scaffold`, attaches the drawer |
| `Drawer()`        | Widget used to build the drawer             |
| `DrawerHeader()`  | Optional top section for profile/info       |
| `ListTile()`      | Common widget used for drawer menu items    |
| `Navigator.pop()` | Closes the drawer when an item is selected  |

---

## 🖼️ UI Behavior

* The **hamburger icon** appears automatically in the `AppBar` when `drawer:` is used.
* The drawer **slides from the left**.
* Tapping anywhere outside or swiping left **closes the drawer**.

---

## 🛠️ Add Right-Side Drawer

You can also add a **right-side drawer** using `endDrawer`:

```dart
Scaffold(
  appBar: AppBar(title: Text('End Drawer')),
  endDrawer: Drawer(
    child: ListView(
      children: [/* items */],
    ),
  ),
)
```

---

## 🎨 Style the Drawer

You can customize the `DrawerHeader`, use `UserAccountsDrawerHeader`, add images, background colors, or icons.

```dart
UserAccountsDrawerHeader(
  accountName: Text("Uday Raut"),
  accountEmail: Text("uday@example.com"),
  currentAccountPicture: CircleAvatar(
    backgroundImage: AssetImage("assets/profile.png"),
  ),
)
```

---

## 🧠 Best Practices

* Keep drawer items **simple and minimal**.
* Use icons for **quick identification**.
* Avoid overloading the drawer with too many options.
* Include user-related info (e.g., email/profile) in the header.

---

## ✅ Summary

| Feature         | Implementation                                   |
| --------------- | ------------------------------------------------ |
| Attach drawer   | `drawer: Drawer(...)` in `Scaffold`              |
| Add items       | Use `ListView` and `ListTile`                    |
| Close drawer    | Use `Navigator.pop(context)`                     |
| Right-side menu | Use `endDrawer`                                  |
| User info       | Use `DrawerHeader` or `UserAccountsDrawerHeader` |

---

 