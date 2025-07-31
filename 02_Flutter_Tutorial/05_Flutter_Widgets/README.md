# 🧱 5. Flutter Widgets

## ➤ StatelessWidget

## ➤ StatefulWidget

In Flutter, **everything is a widget**: buttons, text, rows, columns, containers, even the whole app.

---

## 🎯 What is a Widget?

A **widget** in Flutter is an immutable description of part of the user interface. Flutter uses widgets to build its UI — each widget defines a part of the UI (e.g., a button, padding, layout).

There are **two main types**:

| Type              | Description                                  | UI Can Change? |
| ----------------- | -------------------------------------------- | -------------- |
| `StatelessWidget` | UI that does **not change** over time        | ❌ No           |
| `StatefulWidget`  | UI that **can change** based on events/state | ✅ Yes          |

---

## 🔹 1. StatelessWidget (Static UI)

### 🔸 Definition:

A `StatelessWidget` is a widget **whose properties don’t change once it's built**. It's ideal for UI elements that remain the same.

### 🔸 Example Use Cases:

* Static Text
* Logo or images
* Icons
* Buttons with no state

### 🧪 Example Code:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HelloWidget(),
    );
  }
}

class HelloWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Stateless Widget")),
      body: Center(child: Text("Hello, Uday!")),
    );
  }
}
```

### 🔍 Key Characteristics:

* Extends `StatelessWidget`
* Overrides the `build()` method
* Doesn’t use or manage `State`
* Re-rendered only when parent rebuilds

---

## 🔹 2. StatefulWidget (Dynamic UI)

### 🔸 Definition:

A `StatefulWidget` can **dynamically update its UI** when some data or interaction changes. It has a **separate State object** to store mutable data.

### 🔸 Example Use Cases:

* Toggle switches
* Form input fields
* Counters
* Animations
* Real-time data updates

### 🧪 Example Code:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CounterWidget(),
    );
  }
}

class CounterWidget extends StatefulWidget {
  @override
  _CounterWidgetState createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State<CounterWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++; // Trigger UI rebuild
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Stateful Widget")),
      body: Center(child: Text('Count: $_counter')),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

### 🔍 Key Characteristics:

* Extends `StatefulWidget`
* Has a `State` class (e.g., `_CounterWidgetState`)
* UI rebuilds via `setState()`
* Good for dynamic behavior, input, interaction

---

## 🧠 StatefulWidget vs StatelessWidget – Key Differences

| Feature        | StatelessWidget             | StatefulWidget                  |
| -------------- | --------------------------- | ------------------------------- |
| State Change   | ❌ Not possible              | ✅ Possible with `setState()`    |
| Performance    | ✅ Slightly better (lighter) | ⏳ Slightly heavier              |
| Usage          | Static content              | Dynamic content                 |
| Code Structure | Simple                      | Requires two classes            |
| Examples       | Text, Icon, Image           | Form, Counter, Animation, Input |

---

## 🎯 When to Use Which?

| Scenario                                  | Widget Type       |
| ----------------------------------------- | ----------------- |
| Show a static label                       | `StatelessWidget` |
| Change UI on button click                 | `StatefulWidget`  |
| Display image fetched from network        | `StatefulWidget`  |
| A layout that won’t ever change           | `StatelessWidget` |
| A counter, toggle switch, or progress bar | `StatefulWidget`  |

---

## ✅ Summary

| Concept         | StatelessWidget   | StatefulWidget                   |
| --------------- | ----------------- | -------------------------------- |
| Class Extension | `StatelessWidget` | `StatefulWidget` + `State` class |
| Can update UI?  | ❌ No              | ✅ Yes (via `setState()`)         |
| Ideal for       | Static UI         | Dynamic, interactive UI          |

---

 
# 🧱 Common Widgets in Flutter

## ➤ `Text` Widget

## ➤ `Image` Widget

These are fundamental for displaying content in your app’s UI.

---

## 📌 1. `Text` Widget

### 🔹 Purpose:

Used to display a **string of text** with optional styling, alignment, overflow control, and direction.

---

### ✅ Basic Usage:

```dart
Text("Hello, Uday!");
```

---

### 🔧 Important Properties of `Text`:

| Property        | Description                                    |
| --------------- | ---------------------------------------------- |
| `style`         | Set font size, color, weight, etc.             |
| `textAlign`     | Aligns the text (left, right, center)          |
| `overflow`      | Handles text that doesn’t fit (e.g., ellipsis) |
| `maxLines`      | Limits number of lines                         |
| `softWrap`      | Whether text wraps if too long                 |
| `textDirection` | LTR or RTL                                     |

---

### 🧪 Example:

```dart
Text(
  "Flutter is amazing!",
  style: TextStyle(
    fontSize: 24,
    fontWeight: FontWeight.bold,
    color: Colors.deepPurple,
    letterSpacing: 1.5,
  ),
  textAlign: TextAlign.center,
  maxLines: 1,
  overflow: TextOverflow.ellipsis,
)
```

---

### 🎯 Tips:

* Use `RichText` for multiple styles in one line.
* Use `DefaultTextStyle` to apply styling to multiple texts.

---

## 📌 2. `Image` Widget

### 🔹 Purpose:

Used to display images from various sources — assets, network, memory, file, etc.

---

### ✅ Basic Usage:

```dart
Image.asset("assets/images/logo.png")
Image.network("https://example.com/logo.png")
```

---

### 📦 Image Types:

| Widget Name     | Source Type   | Example                 |
| --------------- | ------------- | ----------------------- |
| `Image.asset`   | App assets    | Local images in project |
| `Image.network` | From internet | CDN, URL-based          |
| `Image.file`    | Device file   | User's gallery/photo    |
| `Image.memory`  | From bytes    | Uint8List in memory     |

---

### 🔧 Important Properties of `Image`:

| Property          | Description                  |
| ----------------- | ---------------------------- |
| `fit`             | How the image fits (BoxFit)  |
| `width`, `height` | Size control                 |
| `alignment`       | Image position               |
| `color`           | Apply color filter           |
| `repeat`          | Repeat the image             |
| `loadingBuilder`  | Shows progress while loading |
| `errorBuilder`    | Handles image load failure   |

---

### 🧪 Example – Image from Network:

```dart
Image.network(
  "https://flutter.dev/images/flutter-logo-sharing.png",
  width: 150,
  height: 150,
  fit: BoxFit.cover,
  loadingBuilder: (context, child, progress) {
    return progress == null
        ? child
        : CircularProgressIndicator();
  },
  errorBuilder: (context, error, stackTrace) {
    return Text("Image not found");
  },
)
```

---

### 🧪 Example – Image from Assets:

1. Add to `pubspec.yaml`:

```yaml
flutter:
  assets:
    - assets/images/myimage.png
```

2. Then use in code:

```dart
Image.asset(
  "assets/images/myimage.png",
  width: 200,
  height: 200,
  fit: BoxFit.contain,
)
```

---

### 🎯 `BoxFit` Options:

| Option      | Description                             |
| ----------- | --------------------------------------- |
| `fill`      | Stretches to fill box                   |
| `contain`   | As large as possible without cropping   |
| `cover`     | Fill box while maintaining aspect ratio |
| `fitWidth`  | Fits width                              |
| `fitHeight` | Fits height                             |
| `none`      | No scaling                              |

---

## ✅ Summary:

| Widget  | Key Use               | Example Source                       |
| ------- | --------------------- | ------------------------------------ |
| `Text`  | Show stylized strings | `Text("Hello")`                      |
| `Image` | Display images        | `Image.asset`, `Image.network`, etc. |

 
---

# 🧱 Common Widgets in Flutter

## ➤ `Icon` Widget

## ➤ `Button` Widgets

### ➤ `ElevatedButton`, `TextButton`, `OutlinedButton`, `IconButton`, `FloatingActionButton`

---

## 🔷 1. `Icon` Widget

### 🔹 Purpose:

Displays a **material design icon** (like home, search, etc.) from Flutter’s **built-in icon set**.

---

### ✅ Basic Usage:

```dart
Icon(Icons.home)
```

---

### 🔧 Important Properties:

| Property        | Description                              |
| --------------- | ---------------------------------------- |
| `icon`          | The icon to display (from `Icons` class) |
| `color`         | Icon color                               |
| `size`          | Size of the icon in logical pixels       |
| `semanticLabel` | Accessibility label                      |
| `textDirection` | Direction for layout if needed           |

---

### 🧪 Example:

```dart
Icon(
  Icons.favorite,
  color: Colors.red,
  size: 40.0,
)
```

---

### 🎯 Bonus Tip:

You can use it inside buttons:

```dart
ElevatedButton.icon(
  onPressed: () {},
  icon: Icon(Icons.send),
  label: Text("Send"),
)
```

---

## 🔷 2. `Button` Widgets

Flutter has **several types** of buttons. All are derived from `StatelessWidget`.

---

### ✅ Types of Buttons in Flutter:

| Button Widget          | Description                        |
| ---------------------- | ---------------------------------- |
| `ElevatedButton`       | Raised button with shadow          |
| `TextButton`           | Flat button with no elevation      |
| `OutlinedButton`       | Bordered button with no fill       |
| `IconButton`           | Button with just an icon           |
| `FloatingActionButton` | Circular button for primary action |

---

### 🔶 A. `ElevatedButton`

#### Basic Usage:

```dart
ElevatedButton(
  onPressed: () {
    print("Button Pressed!");
  },
  child: Text("Click Me"),
)
```

#### With Styling:

```dart
ElevatedButton(
  onPressed: () {},
  child: Text("Styled"),
  style: ElevatedButton.styleFrom(
    primary: Colors.green,
    onPrimary: Colors.white,
    padding: EdgeInsets.symmetric(horizontal: 32, vertical: 16),
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.circular(10),
    ),
  ),
)
```

---

### 🔶 B. `TextButton`

#### Use Case: Minimal button (no elevation)

```dart
TextButton(
  onPressed: () {},
  child: Text("Login"),
)
```

#### With Styling:

```dart
TextButton(
  onPressed: () {},
  child: Text("Custom TextButton"),
  style: TextButton.styleFrom(
    primary: Colors.purple,
    padding: EdgeInsets.all(16),
  ),
)
```

---

### 🔶 C. `OutlinedButton`

#### Use Case: Border-only button

```dart
OutlinedButton(
  onPressed: () {},
  child: Text("Outlined"),
)
```

#### With Styling:

```dart
OutlinedButton(
  onPressed: () {},
  child: Text("Custom Outline"),
  style: OutlinedButton.styleFrom(
    side: BorderSide(color: Colors.blue, width: 2),
    shape: StadiumBorder(),
    padding: EdgeInsets.symmetric(horizontal: 24, vertical: 12),
  ),
)
```

---

### 🔶 D. `IconButton`

#### Use Case: Tappable icon

```dart
IconButton(
  onPressed: () {},
  icon: Icon(Icons.thumb_up),
  color: Colors.blue,
  tooltip: "Like",
)
```

#### Commonly used in `AppBar`, `ListTile`, etc.

---

### 🔶 E. `FloatingActionButton`

#### Use Case: Prominent circular button for primary actions (e.g., add)

```dart
FloatingActionButton(
  onPressed: () {
    print("Add clicked");
  },
  child: Icon(Icons.add),
  backgroundColor: Colors.pink,
)
```

Usually placed using `floatingActionButton` property of `Scaffold`.

```dart
Scaffold(
  floatingActionButton: FloatingActionButton(
    onPressed: () {},
    child: Icon(Icons.add),
  ),
)
```

---

## 🧾 Summary:

| Widget                 | Use Case                        |
| ---------------------- | ------------------------------- |
| `Icon`                 | Display symbols                 |
| `ElevatedButton`       | Raised button (default choice)  |
| `TextButton`           | Flat button (minimal)           |
| `OutlinedButton`       | Button with outline border      |
| `IconButton`           | Tappable icon                   |
| `FloatingActionButton` | Circular button for main action |

---

# 🧱 Common Widgets in Flutter

## ➤ `Scaffold`

## ➤ `AppBar`

With **3-4 practical examples** for each.

---

## 🔷 1. `Scaffold` Widget

### ✅ What is `Scaffold`?

* `Scaffold` provides the **basic visual structure** of a Flutter app.
* It implements the **Material Design layout** structure — like:

  * `AppBar` (top bar),
  * `Drawer` (side menu),
  * `FloatingActionButton`,
  * `BottomNavigationBar`,
  * `Body` content, and more.

---

### 🔧 Key Properties of Scaffold:

| Property                  | Description                             |
| ------------------------- | --------------------------------------- |
| `appBar`                  | Top app bar (usually `AppBar` widget)   |
| `body`                    | Main content area                       |
| `drawer`                  | Left-side navigation drawer             |
| `floatingActionButton`    | Circular button usually at bottom right |
| `bottomNavigationBar`     | Bar at the bottom for switching screens |
| `backgroundColor`         | Scaffold background color               |
| `persistentFooterButtons` | Footer buttons that stay visible        |

---

### 🧪 Example 1: Basic Scaffold

```dart
Scaffold(
  appBar: AppBar(title: Text('My App')),
  body: Center(child: Text('Hello, World!')),
)
```

---

### 🧪 Example 2: Scaffold with `FloatingActionButton`

```dart
Scaffold(
  appBar: AppBar(title: Text('FAB Example')),
  body: Center(child: Text('Click the button!')),
  floatingActionButton: FloatingActionButton(
    onPressed: () => print('Button clicked'),
    child: Icon(Icons.add),
  ),
)
```

---

### 🧪 Example 3: Scaffold with `Drawer`

```dart
Scaffold(
  appBar: AppBar(title: Text('Drawer Example')),
  drawer: Drawer(
    child: ListView(
      children: [
        DrawerHeader(child: Text('Menu')),
        ListTile(title: Text('Home')),
        ListTile(title: Text('Settings')),
      ],
    ),
  ),
  body: Center(child: Text('Swipe from left to open drawer')),
)
```

---

### 🧪 Example 4: Scaffold with `bottomNavigationBar`

```dart
Scaffold(
  appBar: AppBar(title: Text('Bottom Nav Example')),
  body: Center(child: Text('Main content')),
  bottomNavigationBar: BottomNavigationBar(
    items: [
      BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
      BottomNavigationBarItem(icon: Icon(Icons.person), label: 'Profile'),
    ],
  ),
)
```

---

## 🔷 2. `AppBar` Widget

### ✅ What is `AppBar`?

* `AppBar` is a **top bar** used for titles, navigation, actions, etc.
* Commonly used inside the `Scaffold.appBar` property.

---

### 🔧 Key Properties of AppBar:

| Property          | Description                                 |
| ----------------- | ------------------------------------------- |
| `title`           | Widget to show title text                   |
| `leading`         | Left-most widget (e.g., back or menu icon)  |
| `actions`         | Right-side buttons/icons                    |
| `backgroundColor` | Sets app bar background color               |
| `centerTitle`     | Aligns title in the center (default: false) |
| `elevation`       | Shadow depth of app bar                     |

---

### 🧪 Example 1: Basic AppBar

```dart
AppBar(
  title: Text("Simple AppBar"),
)
```

---

### 🧪 Example 2: AppBar with Actions

```dart
AppBar(
  title: Text("Actions Example"),
  actions: [
    IconButton(
      icon: Icon(Icons.search),
      onPressed: () => print("Search tapped"),
    ),
    IconButton(
      icon: Icon(Icons.settings),
      onPressed: () => print("Settings tapped"),
    ),
  ],
)
```

---

### 🧪 Example 3: AppBar with Leading Icon (e.g., back/menu)

```dart
AppBar(
  title: Text("Leading Icon"),
  leading: Icon(Icons.menu),
)
```

---

### 🧪 Example 4: AppBar with Custom Styling

```dart
AppBar(
  title: Text("Styled AppBar"),
  backgroundColor: Colors.deepPurple,
  centerTitle: true,
  elevation: 10.0,
)
```

---

## 🧾 Summary:

| Widget     | Purpose                                             |
| ---------- | --------------------------------------------------- |
| `Scaffold` | Provides overall app structure (body, drawer, etc.) |
| `AppBar`   | Adds top navigation bar with title, icons, etc.     |

These two widgets are **essential for any Flutter screen layout**, especially when using Material Design UI.

---

 # 🌟 Common Widgets in Flutter

## ➤ `Column`

## ➤ `Row`

With **concepts, properties, and 3–4 practical examples** each.

---

## 🔷 1. `Column` Widget

### ✅ What is `Column`?

* A `Column` arranges its children **vertically** (from top to bottom).
* Think of it as a vertical layout manager.

---

### 🔧 Key Properties of Column:

| Property             | Description                                                            |
| -------------------- | ---------------------------------------------------------------------- |
| `children`           | List of widgets inside the column                                      |
| `mainAxisAlignment`  | Vertical alignment (main axis) — like `start`, `center`, `spaceEvenly` |
| `crossAxisAlignment` | Horizontal alignment (cross axis) — like `start`, `end`, `stretch`     |
| `mainAxisSize`       | Decides if column takes **min** or **max** vertical space              |
| `textDirection`      | Defines order of child layout (e.g., `ltr`, `rtl`)                     |

---

### 🧪 Example 1: Simple Column

```dart
Column(
  children: [
    Text('One'),
    Text('Two'),
    Text('Three'),
  ],
)
```

---

### 🧪 Example 2: Column with Centered Content

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    Icon(Icons.star, size: 40),
    Text('Centered Column'),
  ],
)
```

---

### 🧪 Example 3: Column with `spaceAround` Alignment

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  children: [
    Icon(Icons.home),
    Icon(Icons.favorite),
    Icon(Icons.settings),
  ],
)
```

---

### 🧪 Example 4: Nested Column with Containers

```dart
Column(
  children: [
    Container(height: 50, color: Colors.red),
    Container(height: 50, color: Colors.green),
    Container(height: 50, color: Colors.blue),
  ],
)
```

---

## 🔷 2. `Row` Widget

### ✅ What is `Row`?

* A `Row` arranges its children **horizontally** (left to right).
* It works similarly to `Column`, but the main axis is horizontal.

---

### 🔧 Key Properties of Row:

| Property             | Description                                                               |
| -------------------- | ------------------------------------------------------------------------- |
| `children`           | List of widgets inside the row                                            |
| `mainAxisAlignment`  | Horizontal alignment (main axis) — like `start`, `center`, `spaceBetween` |
| `crossAxisAlignment` | Vertical alignment (cross axis) — like `start`, `end`, `stretch`          |
| `mainAxisSize`       | Defines if Row takes **min** or **max** horizontal space                  |

---

### 🧪 Example 1: Simple Row

```dart
Row(
  children: [
    Text('A'),
    Text('B'),
    Text('C'),
  ],
)
```

---

### 🧪 Example 2: Row with Centered Items

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
    Icon(Icons.star),
    Text('Centered Row'),
  ],
)
```

---

### 🧪 Example 3: Row with `spaceEvenly`

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: [
    Icon(Icons.call),
    Icon(Icons.message),
    Icon(Icons.email),
  ],
)
```

---

### 🧪 Example 4: Row with `Expanded` and `Flexible`

```dart
Row(
  children: [
    Expanded(child: Container(height: 50, color: Colors.orange)),
    Flexible(child: Container(height: 50, color: Colors.purple)),
  ],
)
```

---

## 📌 Summary Table

| Widget | Arranges children | Main Axis     | Typical Use Case                           |
| ------ | ----------------- | ------------- | ------------------------------------------ |
| Column | Vertically        | Top to bottom | List of items, forms, stacks               |
| Row    | Horizontally      | Left to right | Icon with text, navigation menus, toolbars |

---

## 🧠 Key Notes:

* Use `Expanded` or `Flexible` inside `Row`/`Column` to control spacing or stretching.
* `mainAxisAlignment` handles **spacing** along the primary axis.
* `crossAxisAlignment` handles **alignment** on the opposite axis.

---

# 🌟 Common Widgets in Flutter

## ➤ `Container`

## ➤ `Padding`

Each will be explained with purpose, properties, and **3–4 practical examples**.

---

## 🔷 1. `Container` Widget

### ✅ What is `Container`?

A `Container` is a versatile widget used to **contain**, **style**, and **position** child widgets. It’s like a box that can hold one child and allows decoration, padding, margin, alignment, size, etc.

---

### 🔧 Key Properties of `Container`:

| Property           | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `child`            | The widget inside the container                          |
| `width` / `height` | Size of the container                                    |
| `color`            | Background color                                         |
| `alignment`        | Align the child within container                         |
| `margin`           | Outer spacing (outside the container)                    |
| `padding`          | Inner spacing (inside, between child and container edge) |
| `decoration`       | Advanced styling like border, gradient, radius           |

---

### 🧪 Example 1: Simple Colored Container

```dart
Container(
  color: Colors.blue,
  width: 200,
  height: 100,
  child: Center(child: Text('Hello Container')),
)
```

---

### 🧪 Example 2: Container with Padding and Margin

```dart
Container(
  margin: EdgeInsets.all(20),
  padding: EdgeInsets.all(10),
  color: Colors.greenAccent,
  child: Text('With Padding & Margin'),
)
```

---

### 🧪 Example 3: Container with Border and Rounded Corners

```dart
Container(
  decoration: BoxDecoration(
    color: Colors.white,
    border: Border.all(color: Colors.black, width: 2),
    borderRadius: BorderRadius.circular(12),
  ),
  padding: EdgeInsets.all(16),
  child: Text('Stylish Container'),
)
```

---

### 🧪 Example 4: Container with Gradient Background

```dart
Container(
  width: 200,
  height: 100,
  decoration: BoxDecoration(
    gradient: LinearGradient(
      colors: [Colors.purple, Colors.blue],
    ),
    borderRadius: BorderRadius.circular(15),
  ),
  child: Center(child: Text('Gradient Box')),
)
```

---

## 🔷 2. `Padding` Widget

### ✅ What is `Padding`?

`Padding` adds **space around its child** from the inside. It doesn't have decoration or background, unlike `Container`.

---

### 🔧 Key Properties of `Padding`:

| Property  | Description                                                            |
| --------- | ---------------------------------------------------------------------- |
| `padding` | Space around the child (`EdgeInsets.all`, `.only`, `.symmetric`, etc.) |
| `child`   | The inner widget being padded                                          |

---

### 🧪 Example 1: Simple Padding Around Text

```dart
Padding(
  padding: EdgeInsets.all(20),
  child: Text('Padded Text'),
)
```

---

### 🧪 Example 2: Padding with Different Sides

```dart
Padding(
  padding: EdgeInsets.only(left: 10, top: 30, right: 10),
  child: Text('Custom Padding'),
)
```

---

### 🧪 Example 3: Padding Inside a Container

```dart
Container(
  color: Colors.yellow,
  child: Padding(
    padding: EdgeInsets.symmetric(horizontal: 30, vertical: 15),
    child: Text('Inside Container'),
  ),
)
```

---

### 🧪 Example 4: Using Padding in Layouts (Row/Column)

```dart
Column(
  children: [
    Padding(
      padding: EdgeInsets.all(8),
      child: Text('Item 1'),
    ),
    Padding(
      padding: EdgeInsets.all(8),
      child: Text('Item 2'),
    ),
  ],
)
```

---

## 📌 Summary Table

| Widget      | Purpose                            | Styling? | Background? |
| ----------- | ---------------------------------- | -------- | ----------- |
| `Container` | Layout, style, size, decoration    | Yes      | Yes         |
| `Padding`   | Adds internal spacing around child | No       | No          |

---

## 🧠 Tips:

* Use `Padding` when you only need **spacing**, not decoration.
* Use `Container` for **more control**: size, background, borders, etc.
* You can **nest** both for better control:

```dart
Padding(
  padding: EdgeInsets.all(10),
  child: Container(
    color: Colors.teal,
    child: Text('Combined Usage'),
  ),
)
```

 
# 🌟 Common Widgets in Flutter

## ➤ `Stack`

## ➤ `Card`

Each section below includes definitions, key properties, and **3–4 practical examples** for better understanding.

---

## 🔷 1. `Stack` Widget

### ✅ What is `Stack`?

The `Stack` widget **allows children to overlap each other**, which is helpful when building UI like banners, watermarks, floating buttons, or custom designs.

It works like layers in Photoshop or Figma — elements are placed on top of each other.

---

### 🔧 Key Properties of `Stack`:

| Property       | Description                                              |
| -------------- | -------------------------------------------------------- |
| `children`     | List of widgets to be stacked                            |
| `alignment`    | Aligns children in the stack (e.g., `Alignment.center`)  |
| `fit`          | How the stack fits the children (e.g., `StackFit.loose`) |
| `clipBehavior` | Clipping behavior when children overflow                 |

---

### 🧪 Example 1: Simple Stack with Overlapping Containers

```dart
Stack(
  children: [
    Container(width: 200, height: 200, color: Colors.blue),
    Container(width: 150, height: 150, color: Colors.red.withOpacity(0.7)),
    Container(width: 100, height: 100, color: Colors.green.withOpacity(0.7)),
  ],
)
```

---

### 🧪 Example 2: Stack with Positioned Widgets

```dart
Stack(
  children: [
    Container(width: 300, height: 200, color: Colors.grey),
    Positioned(
      top: 20,
      left: 30,
      child: Text('Top Left', style: TextStyle(fontSize: 20)),
    ),
    Positioned(
      bottom: 10,
      right: 10,
      child: Icon(Icons.star, color: Colors.yellow, size: 40),
    ),
  ],
)
```

---

### 🧪 Example 3: Image with Overlay Text

```dart
Stack(
  children: [
    Image.network('https://picsum.photos/300/200', width: 300, height: 200, fit: BoxFit.cover),
    Positioned(
      bottom: 10,
      left: 10,
      child: Text('Beautiful Image', style: TextStyle(color: Colors.white, fontSize: 18)),
    ),
  ],
)
```

---

### 🧪 Example 4: Floating Button over Content

```dart
Stack(
  alignment: Alignment.bottomRight,
  children: [
    Container(height: 200, color: Colors.lightBlue),
    FloatingActionButton(
      onPressed: () {},
      child: Icon(Icons.add),
    ),
  ],
)
```

---

## 🔷 2. `Card` Widget

### ✅ What is `Card`?

A `Card` is a widget that displays content inside a **material design panel** with **rounded corners, elevation (shadow)**, and padding. It is used for organizing UI into beautiful blocks.

---

### 🔧 Key Properties of `Card`:

| Property    | Description                  |
| ----------- | ---------------------------- |
| `child`     | The widget inside the card   |
| `elevation` | Shadow depth (z-axis)        |
| `shape`     | Border shape (e.g., rounded) |
| `color`     | Background color             |
| `margin`    | Space outside the card       |

---

### 🧪 Example 1: Simple Card with Text

```dart
Card(
  child: Padding(
    padding: EdgeInsets.all(16),
    child: Text('This is a Card'),
  ),
)
```

---

### 🧪 Example 2: Card with Elevated Shadow and Color

```dart
Card(
  elevation: 8,
  color: Colors.amber[100],
  child: Padding(
    padding: EdgeInsets.all(20),
    child: Text('Card with elevation and color'),
  ),
)
```

---

### 🧪 Example 3: Card with Rounded Corners

```dart
Card(
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(15),
  ),
  elevation: 6,
  child: Padding(
    padding: EdgeInsets.all(16),
    child: Text('Rounded Corner Card'),
  ),
)
```

---

### 🧪 Example 4: Card Containing ListTile

```dart
Card(
  margin: EdgeInsets.all(10),
  child: ListTile(
    leading: Icon(Icons.person),
    title: Text('Uday Raut'),
    subtitle: Text('Flutter Developer'),
    trailing: Icon(Icons.arrow_forward_ios),
  ),
)
```

---

## 📌 Summary Table

| Widget  | Purpose                              | Overlapping Support | Looks Like                |
| ------- | ------------------------------------ | ------------------- | ------------------------- |
| `Stack` | Layout for **overlapping widgets**   | Yes                 | Layered                   |
| `Card`  | Display structured UI blocks (cards) | No                  | Elevated box with styling |

---

## ✅ When to Use

* Use **`Stack`** when you want to **position widgets on top of each other**.
* Use **`Card`** when you want to **group related UI components** with visual elevation.

---
 
# 🌟 Common Widgets: `TextField` & `TextFormField`

---

## 🔷 1. `TextField`

### ✅ What is `TextField`?

The `TextField` widget is used to **take text input** from users. It is simple, lightweight, and used for forms, chat boxes, search bars, etc.

---

### 🔧 Important Properties of `TextField`:

| Property       | Description                                       |
| -------------- | ------------------------------------------------- |
| `controller`   | Used to get or set the current value of the field |
| `decoration`   | For styling (label, hint, icon, border)           |
| `keyboardType` | Type of keyboard (text, number, email, etc.)      |
| `onChanged`    | Callback when the text changes                    |
| `obscureText`  | Hides input (used for passwords)                  |
| `maxLines`     | Number of visible lines                           |
| `enabled`      | Enable/disable field                              |
| `readOnly`     | Makes the field read-only                         |

---

### 🧪 Example 1: Simple Text Input

```dart
TextField(
  decoration: InputDecoration(
    labelText: 'Enter your name',
    border: OutlineInputBorder(),
  ),
)
```

---

### 🧪 Example 2: Password Field

```dart
TextField(
  obscureText: true,
  decoration: InputDecoration(
    labelText: 'Password',
    prefixIcon: Icon(Icons.lock),
    border: OutlineInputBorder(),
  ),
)
```

---

### 🧪 Example 3: Number Input with Icon

```dart
TextField(
  keyboardType: TextInputType.number,
  decoration: InputDecoration(
    labelText: 'Phone Number',
    prefixIcon: Icon(Icons.phone),
    border: OutlineInputBorder(),
  ),
)
```

---

### 🧪 Example 4: Using Controller to Read Text

```dart
TextEditingController _controller = TextEditingController();

Column(
  children: [
    TextField(
      controller: _controller,
      decoration: InputDecoration(labelText: 'Enter city'),
    ),
    ElevatedButton(
      onPressed: () {
        print("Entered: ${_controller.text}");
      },
      child: Text('Submit'),
    )
  ],
)
```

---

## 🔷 2. `TextFormField`

### ✅ What is `TextFormField`?

`TextFormField` is similar to `TextField`, **but built to work inside `Form` widgets**, and provides **form validation** and other advanced form-handling features.

Use `TextFormField` when you need **validation**, **auto-saving**, **form state**, etc.

---

### 🔧 Important Properties of `TextFormField`:

| Property           | Description                        |
| ------------------ | ---------------------------------- |
| `validator`        | Function that validates user input |
| `initialValue`     | Sets initial value of the field    |
| `controller`       | Controls text input                |
| `decoration`       | Same as TextField                  |
| `onSaved`          | Stores value on form submit        |
| `autovalidateMode` | Triggers automatic validation      |

---

### 🧪 Example 1: Simple Validated Form

```dart
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(
        decoration: InputDecoration(labelText: 'Email'),
        validator: (value) {
          if (value == null || value.isEmpty) {
            return 'Please enter email';
          }
          return null;
        },
      ),
      ElevatedButton(
        onPressed: () {
          if (_formKey.currentState!.validate()) {
            print("Form Validated!");
          }
        },
        child: Text('Submit'),
      )
    ],
  ),
)
```

---

### 🧪 Example 2: Password Validator

```dart
TextFormField(
  obscureText: true,
  decoration: InputDecoration(labelText: 'Password'),
  validator: (value) {
    if (value == null || value.length < 6) {
      return 'Password must be at least 6 characters';
    }
    return null;
  },
)
```

---

### 🧪 Example 3: Using `controller` with `TextFormField`

```dart
final TextEditingController nameController = TextEditingController();

TextFormField(
  controller: nameController,
  decoration: InputDecoration(labelText: 'Your Name'),
)
```

---

### 🧪 Example 4: Saving Field Input

```dart
String? savedName;

Form(
  child: TextFormField(
    onSaved: (newValue) => savedName = newValue,
    decoration: InputDecoration(labelText: 'Full Name'),
  ),
)
```

---

## 🧩 Difference Between `TextField` vs `TextFormField`

| Feature             | `TextField`    | `TextFormField`      |
| ------------------- | -------------- | -------------------- |
| Validation          | ❌ Not built-in | ✅ Built-in           |
| Form integration    | ❌ Manual       | ✅ Designed for forms |
| Simpler to use      | ✅ Yes          | ⚠️ More structured   |
| Preferred for Forms | ❌ No           | ✅ Yes                |

---

## ✅ When to Use

* Use **`TextField`** for simple, one-off inputs like search, comments, or messaging.
* Use **`TextFormField`** when you're building a **full form** with validation, submission, and saving logic.

---

  
# ✅ Common Widgets: `Checkbox` and `Radio`

---

## 🔷 1. `Checkbox`

### ✅ What is `Checkbox`?

A `Checkbox` allows users to **select one or more options** from a set. It shows a square box that can be **checked (true)** or **unchecked (false)**.

---

### 🔧 Key Properties of `Checkbox`:

| Property      | Description                               |
| ------------- | ----------------------------------------- |
| `value`       | Current state (`true` or `false`)         |
| `onChanged`   | Callback when state changes               |
| `activeColor` | Color when checkbox is checked            |
| `checkColor`  | Color of the checkmark                    |
| `tristate`    | Allows `true`, `false`, and `null` values |

---

### 🧪 Example 1: Basic Checkbox

```dart
bool isChecked = false;

Checkbox(
  value: isChecked,
  onChanged: (bool? newValue) {
    setState(() {
      isChecked = newValue!;
    });
  },
)
```

---

### 🧪 Example 2: Checkbox with Label using `CheckboxListTile`

```dart
CheckboxListTile(
  title: Text("I accept terms & conditions"),
  value: isChecked,
  onChanged: (bool? newValue) {
    setState(() {
      isChecked = newValue!;
    });
  },
)
```

---

### 🧪 Example 3: Multiple Checkboxes

```dart
bool isEmailChecked = false;
bool isSMSChecked = false;

Column(
  children: [
    CheckboxListTile(
      title: Text("Email Notifications"),
      value: isEmailChecked,
      onChanged: (bool? value) {
        setState(() {
          isEmailChecked = value!;
        });
      },
    ),
    CheckboxListTile(
      title: Text("SMS Notifications"),
      value: isSMSChecked,
      onChanged: (bool? value) {
        setState(() {
          isSMSChecked = value!;
        });
      },
    ),
  ],
)
```

---

### 🧪 Example 4: Custom Checkbox Colors

```dart
Checkbox(
  value: isChecked,
  onChanged: (bool? value) {
    setState(() {
      isChecked = value!;
    });
  },
  activeColor: Colors.green,
  checkColor: Colors.white,
)
```

---

## 🔷 2. `Radio`

### ✅ What is `Radio`?

A `Radio` widget allows the user to **select only one option** from a list. Ideal when you have 2–5 exclusive options (like gender, payment method, etc.).

---

### 🔧 Key Properties of `Radio`:

| Property     | Description                           |
| ------------ | ------------------------------------- |
| `value`      | Value assigned to this radio button   |
| `groupValue` | Currently selected value of the group |
| `onChanged`  | Callback to update selection          |

---

### 🧪 Example 1: Simple Radio Buttons

```dart
String gender = 'male';

Column(
  children: [
    Radio(
      value: 'male',
      groupValue: gender,
      onChanged: (String? value) {
        setState(() {
          gender = value!;
        });
      },
    ),
    Radio(
      value: 'female',
      groupValue: gender,
      onChanged: (String? value) {
        setState(() {
          gender = value!;
        });
      },
    ),
  ],
)
```

---

### 🧪 Example 2: Using `RadioListTile` (Better UI)

```dart
RadioListTile(
  title: Text("Male"),
  value: "male",
  groupValue: gender,
  onChanged: (String? value) {
    setState(() {
      gender = value!;
    });
  },
),

RadioListTile(
  title: Text("Female"),
  value: "female",
  groupValue: gender,
  onChanged: (String? value) {
    setState(() {
      gender = value!;
    });
  },
),
```

---

### 🧪 Example 3: Custom Colored Radio Button

```dart
Radio(
  value: "other",
  groupValue: gender,
  activeColor: Colors.orange,
  onChanged: (String? value) {
    setState(() {
      gender = value!;
    });
  },
)
```

---

### 🧪 Example 4: Radio inside a ListView

```dart
List<String> paymentOptions = ["Credit Card", "Debit Card", "UPI"];
String selectedPayment = "UPI";

ListView.builder(
  itemCount: paymentOptions.length,
  itemBuilder: (context, index) {
    return RadioListTile(
      title: Text(paymentOptions[index]),
      value: paymentOptions[index],
      groupValue: selectedPayment,
      onChanged: (value) {
        setState(() {
          selectedPayment = value!;
        });
      },
    );
  },
)
```

---

## 🧩 Difference Between `Checkbox` vs `Radio`

| Feature           | `Checkbox`                     | `Radio`                  |
| ----------------- | ------------------------------ | ------------------------ |
| Type of Selection | Multiple Choices               | Single Exclusive Choice  |
| UI                | Square tick-box                | Circular bullet selector |
| Widget Variants   | `Checkbox`, `CheckboxListTile` | `Radio`, `RadioListTile` |

---


# ✅ Common Widgets: `Switch` and `Slider`

---

## 🔷 1. `Switch`

### ✅ What is `Switch`?

A `Switch` widget in Flutter represents a **toggle button**. It is used for turning options **on or off**, similar to real-world light switches or toggle buttons in mobile settings (like WiFi, Bluetooth, etc.).

---

### 🔧 Key Properties of `Switch`:

| Property             | Description                                       |
| -------------------- | ------------------------------------------------- |
| `value`              | Boolean – current state of switch (true or false) |
| `onChanged`          | Callback triggered when switch is toggled         |
| `activeColor`        | Color of the switch when it's ON                  |
| `inactiveThumbColor` | Color of the thumb when it's OFF                  |
| `activeTrackColor`   | Track color when the switch is ON                 |
| `inactiveTrackColor` | Track color when the switch is OFF                |

---

### 🧪 Example 1: Basic Switch

```dart
bool isSwitched = false;

Switch(
  value: isSwitched,
  onChanged: (bool value) {
    setState(() {
      isSwitched = value;
    });
  },
)
```

---

### 🧪 Example 2: Switch with Label (using `ListTile`)

```dart
ListTile(
  title: Text("Enable Dark Mode"),
  trailing: Switch(
    value: isSwitched,
    onChanged: (bool value) {
      setState(() {
        isSwitched = value;
      });
    },
  ),
)
```

---

### 🧪 Example 3: Custom Colored Switch

```dart
Switch(
  value: isSwitched,
  onChanged: (bool value) {
    setState(() {
      isSwitched = value;
    });
  },
  activeColor: Colors.green,
  inactiveThumbColor: Colors.grey,
  activeTrackColor: Colors.greenAccent,
)
```

---

### 🧪 Example 4: Multiple Settings Toggles

```dart
bool wifi = false;
bool bluetooth = true;

Column(
  children: [
    SwitchListTile(
      title: Text("Wi-Fi"),
      value: wifi,
      onChanged: (val) => setState(() => wifi = val),
    ),
    SwitchListTile(
      title: Text("Bluetooth"),
      value: bluetooth,
      onChanged: (val) => setState(() => bluetooth = val),
    ),
  ],
)
```

---

## 🔷 2. `Slider`

### ✅ What is `Slider`?

A `Slider` widget in Flutter allows users to **select a value from a range** by sliding a thumb horizontally. It's commonly used for settings like volume, brightness, rating, etc.

---

### 🔧 Key Properties of `Slider`:

| Property        | Description                          |
| --------------- | ------------------------------------ |
| `value`         | Current value of the slider (double) |
| `onChanged`     | Callback when user slides the thumb  |
| `min`           | Minimum value                        |
| `max`           | Maximum value                        |
| `divisions`     | Number of discrete divisions         |
| `label`         | Label shown while sliding            |
| `activeColor`   | Color of active part of the slider   |
| `inactiveColor` | Color of inactive part               |

---

### 🧪 Example 1: Basic Slider

```dart
double _sliderValue = 20;

Slider(
  value: _sliderValue,
  min: 0,
  max: 100,
  onChanged: (double value) {
    setState(() {
      _sliderValue = value;
    });
  },
)
```

---

### 🧪 Example 2: Slider with Label and Divisions

```dart
Slider(
  value: _sliderValue,
  min: 0,
  max: 10,
  divisions: 10,
  label: _sliderValue.round().toString(),
  onChanged: (double value) {
    setState(() {
      _sliderValue = value;
    });
  },
)
```

---

### 🧪 Example 3: Colored Slider

```dart
Slider(
  value: _sliderValue,
  min: 0,
  max: 100,
  onChanged: (double value) {
    setState(() {
      _sliderValue = value;
    });
  },
  activeColor: Colors.purple,
  inactiveColor: Colors.purple.shade100,
)
```

---

### 🧪 Example 4: Use Slider for Volume Control

```dart
double volume = 0.5;

Column(
  children: [
    Text("Volume: ${(volume * 100).round()}%"),
    Slider(
      value: volume,
      min: 0.0,
      max: 1.0,
      divisions: 10,
      label: (volume * 100).round().toString(),
      onChanged: (val) {
        setState(() {
          volume = val;
        });
      },
    ),
  ],
)
```

---

## 🔁 Summary

| Widget   | Purpose                 | Example Use                 |
| -------- | ----------------------- | --------------------------- |
| `Switch` | Toggle ON/OFF values    | Wi-Fi, Bluetooth, Dark mode |
| `Slider` | Pick a value in a range | Volume, Brightness, Ratings |


## 👉 GestureDetector & InkWell

These widgets allow your app to respond to **user gestures** like taps, double taps, long presses, swipes, and more.

---

## 🔷 1. `GestureDetector`

### ✅ What is `GestureDetector`?

The `GestureDetector` is a **non-visual widget** that detects gestures made by the user and executes functions (callbacks) in response.

### 📌 Common Gestures Supported:

| Gesture         | Callback Function        |
| --------------- | ------------------------ |
| Tap             | `onTap`                  |
| Double Tap      | `onDoubleTap`            |
| Long Press      | `onLongPress`            |
| Pan (drag)      | `onPanUpdate`            |
| Vertical Drag   | `onVerticalDragUpdate`   |
| Horizontal Drag | `onHorizontalDragUpdate` |

---

### 🧪 Example 1: Tap on a Container

```dart
GestureDetector(
  onTap: () {
    print('Container tapped!');
  },
  child: Container(
    color: Colors.blue,
    height: 100,
    width: 100,
    child: Center(child: Text("Tap Me")),
  ),
)
```

---

### 🧪 Example 2: Detect Long Press

```dart
GestureDetector(
  onLongPress: () {
    print('Long pressed!');
  },
  child: Icon(Icons.favorite, size: 50, color: Colors.red),
)
```

---

### 🧪 Example 3: Swipe to Update Position

```dart
GestureDetector(
  onPanUpdate: (details) {
    print('Swiped: ${details.delta}');
  },
  child: Container(
    width: 200,
    height: 100,
    color: Colors.orange,
    child: Center(child: Text("Swipe Me")),
  ),
)
```

---

### 🧪 Example 4: Double Tap Zoom Effect (Concept)

```dart
GestureDetector(
  onDoubleTap: () {
    setState(() {
      _zoomed = !_zoomed;
    });
  },
  child: AnimatedContainer(
    duration: Duration(milliseconds: 300),
    width: _zoomed ? 300 : 150,
    height: _zoomed ? 300 : 150,
    color: Colors.green,
    child: Center(child: Text("Double Tap")),
  ),
)
```

---

## 🔷 2. `InkWell`

### ✅ What is `InkWell`?

`InkWell` is similar to `GestureDetector` but **includes a ripple effect** when tapped. It's used when you want your widget to **look tappable**, like buttons, list items, etc.

It must be a **child of a Material widget** to show the ripple.

---

### 🧪 Example 1: InkWell on a Container

```dart
InkWell(
  onTap: () {
    print('InkWell tapped');
  },
  child: Container(
    width: 150,
    height: 80,
    color: Colors.yellow,
    child: Center(child: Text("Tap Me")),
  ),
)
```

---

### 🧪 Example 2: Ripple on Image

```dart
InkWell(
  onTap: () {
    print('Image tapped');
  },
  child: Image.network('https://via.placeholder.com/150'),
)
```

---

### 🧪 Example 3: ListTile with InkWell

```dart
Material(
  child: InkWell(
    onTap: () {
      print("Tapped list item");
    },
    child: ListTile(
      title: Text("Click Me"),
      subtitle: Text("With ripple effect"),
    ),
  ),
)
```

---

### 🧪 Example 4: Custom Button with InkWell

```dart
Material(
  color: Colors.transparent,
  child: InkWell(
    onTap: () {
      print('Custom button tapped');
    },
    borderRadius: BorderRadius.circular(12),
    child: Container(
      padding: EdgeInsets.all(16),
      decoration: BoxDecoration(
        color: Colors.teal,
        borderRadius: BorderRadius.circular(12),
      ),
      child: Text("Custom Button", style: TextStyle(color: Colors.white)),
    ),
  ),
)
```

---

## 🔁 Summary Table:

| Feature           | `GestureDetector`                | `InkWell`                            |
| ----------------- | -------------------------------- | ------------------------------------ |
| Tap Detection     | ✅                                | ✅                                    |
| Ripple Effect     | ❌                                | ✅ (with Material ancestor)           |
| Multiple Gestures | ✅ (drag, long press, double tap) | ✅ (mostly tap and long press)        |
| Use Case          | Custom gestures                  | UI elements needing ripple (buttons) |

---

## 🔹 1. **Forms in Flutter**

### ✅ What is a Form?

A **`Form`** widget groups and validates multiple form fields like `TextFormField`, `DropdownButtonFormField`, etc. It's used for **input validation** and **data collection**.

### 📌 Important Elements:

* `Form`: Parent widget that groups form fields.
* `GlobalKey<FormState>`: Used to validate and save the form.
* `TextFormField`: Input field with built-in validation.
* `FormField`: Generic form input if custom control is needed.

---

### 🧪 Example 1: Basic Form with Validation

```dart
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(
        decoration: InputDecoration(labelText: 'Email'),
        validator: (value) {
          if (value == null || value.isEmpty) {
            return 'Enter an email';
          }
          return null;
        },
      ),
      ElevatedButton(
        onPressed: () {
          if (_formKey.currentState!.validate()) {
            print('Form is valid');
          }
        },
        child: Text('Submit'),
      ),
    ],
  ),
)
```

---

### 🧪 Example 2: Form with Multiple Fields

```dart
Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(
        decoration: InputDecoration(labelText: 'Username'),
        validator: (val) => val!.isEmpty ? 'Enter username' : null,
      ),
      TextFormField(
        obscureText: true,
        decoration: InputDecoration(labelText: 'Password'),
        validator: (val) => val!.length < 6 ? 'Min 6 chars' : null,
      ),
      ElevatedButton(onPressed: () {
        if (_formKey.currentState!.validate()) {
          print("Valid Login Form");
        }
      }, child: Text("Login"))
    ],
  ),
)
```

---

### 🧪 Example 3: Using `TextEditingController`

```dart
final nameController = TextEditingController();

Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(
        controller: nameController,
        decoration: InputDecoration(labelText: 'Name'),
      ),
      ElevatedButton(
        onPressed: () {
          print('Name: ${nameController.text}');
        },
        child: Text('Print Name'),
      ),
    ],
  ),
)
```

---

## 🔹 2. **ListView**

### ✅ What is ListView?

`ListView` is a **scrollable list of widgets**. Ideal for displaying dynamic lists, such as items, messages, or product listings.

### 📌 Types of ListViews:

* `ListView()`: Manually define children
* `ListView.builder()`: Efficient for long lists
* `ListView.separated()`: Adds separators
* `ListView.custom()`: Fully customizable

---

### 🧪 Example 1: Basic Vertical List

```dart
ListView(
  children: [
    Text('Item 1'),
    Text('Item 2'),
    Text('Item 3'),
  ],
)
```

---

### 🧪 Example 2: ListView\.builder

```dart
ListView.builder(
  itemCount: 5,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text('Item $index'),
    );
  },
)
```

---

### 🧪 Example 3: Horizontal List

```dart
ListView(
  scrollDirection: Axis.horizontal,
  children: [
    Container(width: 100, color: Colors.red),
    Container(width: 100, color: Colors.blue),
    Container(width: 100, color: Colors.green),
  ],
)
```

---

### 🧪 Example 4: ListView\.separated

```dart
ListView.separated(
  itemCount: 5,
  itemBuilder: (context, index) => ListTile(title: Text("Item $index")),
  separatorBuilder: (context, index) => Divider(),
)
```

---

## 🔹 3. **ListTile**

### ✅ What is ListTile?

`ListTile` is a **ready-made layout widget** used inside lists. It provides:

* `leading` (icon/image)
* `title`
* `subtitle`
* `trailing`
* `onTap`

---

### 🧪 Example 1: Basic ListTile

```dart
ListTile(
  leading: Icon(Icons.person),
  title: Text('Uday Raut'),
  subtitle: Text('Flutter Developer'),
  trailing: Icon(Icons.arrow_forward),
)
```

---

### 🧪 Example 2: ListTile in ListView

```dart
ListView(
  children: [
    ListTile(
      title: Text("Item 1"),
      onTap: () => print("Tapped Item 1"),
    ),
    ListTile(
      title: Text("Item 2"),
      onTap: () => print("Tapped Item 2"),
    ),
  ],
)
```

---

### 🧪 Example 3: ListTile with CircleAvatar

```dart
ListTile(
  leading: CircleAvatar(child: Text("U")),
  title: Text('Uday Raut'),
  subtitle: Text('Cybersecurity | Flutter'),
  trailing: Icon(Icons.call),
)
```

---

### 🧪 Example 4: ListTile as a Setting Option

```dart
ListTile(
  leading: Icon(Icons.settings),
  title: Text("Settings"),
  trailing: Icon(Icons.navigate_next),
  onTap: () {
    Navigator.push(context, MaterialPageRoute(builder: (_) => SettingsPage()));
  },
)
```

---

## 🔁 Summary Table

| Widget     | Purpose                                     |
| ---------- | ------------------------------------------- |
| `Form`     | Handles validation and submission of inputs |
| `ListView` | Displays scrollable list of items           |
| `ListTile` | Pre-built layout for list items             |

---

 