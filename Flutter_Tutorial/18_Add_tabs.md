Adding **tabs** in a Flutter app is a common UI pattern used to allow users to quickly navigate between different views or sections. Flutter provides a flexible way to implement tabs using the `TabBar`, `TabBarView`, and `DefaultTabController` widgets.

---

# 🗂️ Add Tabs to Your Flutter App – Detailed Guide

---

## 📌 Overview

Tabs help organize content across different screens within the same page. Flutter’s tabbed interface uses:

* **`TabBar`** → Displays the set of tabs.
* **`TabBarView`** → Displays content associated with each tab.
* **`DefaultTabController`** → Controls and synchronizes the `TabBar` and `TabBarView`.

---

## 🧱 Basic Tab Structure

```dart
DefaultTabController(
  length: 3, // Number of tabs
  child: Scaffold(
    appBar: AppBar(
      title: Text("Tab Example"),
      bottom: TabBar(
        tabs: [
          Tab(icon: Icon(Icons.home), text: "Home"),
          Tab(icon: Icon(Icons.star), text: "Favorites"),
          Tab(icon: Icon(Icons.settings), text: "Settings"),
        ],
      ),
    ),
    body: TabBarView(
      children: [
        Center(child: Text("Home Page")),
        Center(child: Text("Favorites Page")),
        Center(child: Text("Settings Page")),
      ],
    ),
  ),
);
```

---

## 🧠 Explanation of Key Components

### ✅ `DefaultTabController`

* Manages the state and synchronization of tabs.
* `length`: Number of tabs.

```dart
DefaultTabController(length: 3, child: ...)
```

---

### ✅ `TabBar`

* A horizontal bar of clickable tabs.
* Can include text, icons, or both.

```dart
TabBar(
  tabs: [
    Tab(text: "One"),
    Tab(icon: Icon(Icons.star)),
    Tab(icon: Icon(Icons.settings), text: "Settings"),
  ],
)
```

---

### ✅ `TabBarView`

* The actual content of each tab.
* Must be in the same order as the `TabBar` tabs.

```dart
TabBarView(
  children: [
    Widget1(),
    Widget2(),
    Widget3(),
  ],
)
```

---

## 💡 Tips

### 🌙 Add TabController manually (for custom control)

Use `TabController` if you need more control (e.g. animated transitions or switching tabs programmatically).

```dart
class MyTabPage extends StatefulWidget {
  @override
  _MyTabPageState createState() => _MyTabPageState();
}

class _MyTabPageState extends State<MyTabPage> with SingleTickerProviderStateMixin {
  late TabController _tabController;

  @override
  void initState() {
    super.initState();
    _tabController = TabController(length: 3, vsync: this);
  }

  @override
  void dispose() {
    _tabController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Custom Tabs"),
        bottom: TabBar(
          controller: _tabController,
          tabs: [
            Tab(text: "A"),
            Tab(text: "B"),
            Tab(text: "C"),
          ],
        ),
      ),
      body: TabBarView(
        controller: _tabController,
        children: [
          Text("Tab A"),
          Text("Tab B"),
          Text("Tab C"),
        ],
      ),
    );
  }
}
```

---

## 🌐 Tabs with BottomNavigationBar (Alternative UI)

```dart
class BottomTabsExample extends StatefulWidget {
  @override
  _BottomTabsExampleState createState() => _BottomTabsExampleState();
}

class _BottomTabsExampleState extends State<BottomTabsExample> {
  int _currentIndex = 0;
  final tabs = [
    Center(child: Text("Home")),
    Center(child: Text("Search")),
    Center(child: Text("Profile")),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: tabs[_currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        items: [
          BottomNavigationBarItem(icon: Icon(Icons.home), label: "Home"),
          BottomNavigationBarItem(icon: Icon(Icons.search), label: "Search"),
          BottomNavigationBarItem(icon: Icon(Icons.person), label: "Profile"),
        ],
        onTap: (index) {
          setState(() {
            _currentIndex = index;
          });
        },
      ),
    );
  }
}
```

---

## 🎨 Customize Tab Styles

You can style your tabs using:

```dart
TabBar(
  labelColor: Colors.white,
  unselectedLabelColor: Colors.grey,
  indicatorColor: Colors.yellow,
  indicatorWeight: 4.0,
  tabs: [ ... ],
)
```

---

## ✅ Summary

| Widget                 | Purpose                                   |
| ---------------------- | ----------------------------------------- |
| `DefaultTabController` | Automatically manages tab state           |
| `TabBar`               | UI for tabs (with text or icons)          |
| `TabBarView`           | Content displayed when each tab is active |
| `TabController`        | For manual tab control                    |
| `BottomNavigationBar`  | Alternative to top tabs                   |

---

 