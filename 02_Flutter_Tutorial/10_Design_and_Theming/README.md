## 🔹 1. **Themes and ThemeData**

### ✅ What is it?

`ThemeData` is used to define colors, font styles, icon styles, button appearances, etc., across your entire app for consistency.

### 🔧 How to Apply Theme:

```dart
MaterialApp(
  title: 'Themed App',
  theme: ThemeData(
    primarySwatch: Colors.deepPurple,
    textTheme: TextTheme(
      bodyLarge: TextStyle(fontSize: 18, color: Colors.black),
    ),
  ),
  home: MyHomePage(),
);
```

---

### 📘 Examples:

#### 🧪 Example 1: Access Theme in Widgets

```dart
Text(
  'Hello Flutter',
  style: Theme.of(context).textTheme.bodyLarge,
);
```

---

#### 🧪 Example 2: Customize AppBar Theme

```dart
theme: ThemeData(
  appBarTheme: AppBarTheme(
    backgroundColor: Colors.blueGrey,
    titleTextStyle: TextStyle(color: Colors.white, fontSize: 20),
  ),
),
```

---

#### 🧪 Example 3: Button Styling

```dart
theme: ThemeData(
  elevatedButtonTheme: ElevatedButtonThemeData(
    style: ElevatedButton.styleFrom(
      backgroundColor: Colors.deepPurple,
      textStyle: TextStyle(fontSize: 16),
    ),
  ),
),
```

---

#### 🧪 Example 4: Use ThemeData Extension

```dart
ThemeData base = ThemeData.light();

ThemeData customTheme = base.copyWith(
  primaryColor: Colors.teal,
  textTheme: base.textTheme.copyWith(
    titleLarge: TextStyle(color: Colors.teal),
  ),
);
```

---

## 🔹 2. **Dark & Light Themes**

### ✅ What is it?

Flutter allows switching between **light** and **dark themes** either manually or based on system settings.

---

### 📘 Examples:

#### 🧪 Example 1: Define Light & Dark Theme in `MaterialApp`

```dart
MaterialApp(
  theme: ThemeData.light(),
  darkTheme: ThemeData.dark(),
  themeMode: ThemeMode.system, // light, dark, or system
);
```

---

#### 🧪 Example 2: Manually Toggle Theme

Use `Provider` or `ValueNotifier` to change `ThemeMode`.

```dart
themeMode: _isDark ? ThemeMode.dark : ThemeMode.light,
```

---

#### 🧪 Example 3: Custom Light & Dark ThemeData

```dart
ThemeData light = ThemeData(
  brightness: Brightness.light,
  primarySwatch: Colors.indigo,
);

ThemeData dark = ThemeData(
  brightness: Brightness.dark,
  primarySwatch: Colors.deepOrange,
);
```

---

#### 🧪 Example 4: Access Current Theme in Runtime

```dart
bool isDarkMode = Theme.of(context).brightness == Brightness.dark;
```

---

## 🔹 3. **Custom Fonts and Colors**

### ✅ What is it?

Customize the **typography** and **color palette** of your app to match branding.

---

### 📘 Examples:

#### 🧪 Example 1: Add Custom Font

**pubspec.yaml**:

```yaml
flutter:
  fonts:
    - family: Poppins
      fonts:
        - asset: assets/fonts/Poppins-Regular.ttf
```

In `ThemeData`:

```dart
theme: ThemeData(
  fontFamily: 'Poppins',
),
```

---

#### 🧪 Example 2: Use Custom Color Palette

```dart
const MaterialColor customGreen = MaterialColor(
  0xFF00A86B,
  <int, Color>{
    50: Color(0xFFE0F2F1),
    100: Color(0xFFB2DFDB),
    200: Color(0xFF80CBC4),
    300: Color(0xFF4DB6AC),
    400: Color(0xFF26A69A),
    500: Color(0xFF00A86B), // Main color
    600: Color(0xFF009688),
    700: Color(0xFF00897B),
    800: Color(0xFF00796B),
    900: Color(0xFF004D40),
  },
);

theme: ThemeData(
  primarySwatch: customGreen,
),
```

---

#### 🧪 Example 3: Override TextStyle Per Widget

```dart
Text(
  'Custom Font',
  style: TextStyle(
    fontFamily: 'Poppins',
    fontSize: 24,
    color: Colors.teal,
  ),
),
```

---

#### 🧪 Example 4: Add Theme Extension for Custom Colors

```dart
extension CustomTheme on ThemeData {
  Color get danger => const Color(0xFFE53935);
}

Text(
  'Warning!',
  style: TextStyle(color: Theme.of(context).danger),
);
```

---

## ✅ Summary Table

| Concept               | Description                            | Example Usage                           |
| --------------------- | -------------------------------------- | --------------------------------------- |
| ThemeData             | Global app styling container           | `ThemeData(primarySwatch: Colors.blue)` |
| Dark & Light Themes   | Switch themes by system or manually    | `themeMode: ThemeMode.system`           |
| Custom Fonts & Colors | Use your brand's colors and typography | `fontFamily: 'Poppins'`, custom `Color` |

---
 
## 🔹 1. **MediaQuery**

### ✅ What is MediaQuery?

`MediaQuery` gives information about the current screen size, orientation, device pixel ratio, and more. It’s commonly used for **responsive layouts**.

---

### 🧪 Example 1: Get Screen Width & Height

```dart
double width = MediaQuery.of(context).size.width;
double height = MediaQuery.of(context).size.height;

Text('Screen Width: $width\nScreen Height: $height');
```

---

### 🧪 Example 2: Responsive Font Size

```dart
Text(
  'Responsive Text',
  style: TextStyle(fontSize: MediaQuery.of(context).size.width * 0.05),
);
```

---

### 🧪 Example 3: Layout Based on Orientation

```dart
if (MediaQuery.of(context).orientation == Orientation.portrait) {
  return Column(children: [...]);
} else {
  return Row(children: [...]);
}
```

---

### 🧪 Example 4: Conditional Padding

```dart
Padding(
  padding: EdgeInsets.symmetric(
    horizontal: MediaQuery.of(context).size.width > 600 ? 32 : 16,
  ),
  child: Text("Responsive Padding"),
);
```

---

## 🔹 2. **Responsive Design using LayoutBuilder & FittedBox**

---

### ✅ a) `LayoutBuilder`

Gives the **constraints** (maxWidth, maxHeight) of the parent widget. Useful for **responsive layouts inside containers**.

#### 🧪 Example 1: Adjust UI Based on Width

```dart
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 600) {
      return Row(children: [...]); // Tablet
    } else {
      return Column(children: [...]); // Mobile
    }
  },
);
```

---

### ✅ b) `FittedBox`

Scales and positions its child **within itself** based on fit properties.

#### 🧪 Example 2: FittedBox for Scaling

```dart
FittedBox(
  child: Text(
    'Scalable Text',
    style: TextStyle(fontSize: 50),
  ),
);
```

#### 🧪 Example 3: Image in FittedBox

```dart
FittedBox(
  fit: BoxFit.contain,
  child: Image.asset('assets/logo.png'),
);
```

#### 🧪 Example 4: Button in FittedBox for Small Screens

```dart
FittedBox(
  child: ElevatedButton(
    onPressed: () {},
    child: Text("Click Me"),
  ),
);
```

---

## 🔹 3. **Flutter Responsive Frameworks**

### ✅ Why Use Frameworks?

Responsive frameworks simplify complex device responsiveness (mobile, tablet, desktop) with consistent breakpoints and layout helpers.

---

### ✅ Popular Flutter Responsive Frameworks:

#### ➤ **responsive\_framework**

[Package: `responsive_framework`](https://pub.dev/packages/responsive_framework)

#### 🧪 Example 1: Setup in MaterialApp

```dart
import 'package:responsive_framework/responsive_framework.dart';

MaterialApp(
  builder: (context, child) => ResponsiveWrapper.builder(
    child,
    maxWidth: 1200,
    minWidth: 450,
    defaultScale: true,
    breakpoints: [
      ResponsiveBreakpoint.resize(450, name: MOBILE),
      ResponsiveBreakpoint.autoScale(800, name: TABLET),
      ResponsiveBreakpoint.autoScale(1000, name: DESKTOP),
    ],
  ),
);
```

---

#### 🧪 Example 2: Use `ResponsiveRowColumn`

```dart
ResponsiveRowColumn(
  rowMainAxisAlignment: MainAxisAlignment.center,
  layout: ResponsiveWrapper.of(context).isSmallerThan(TABLET)
      ? ResponsiveRowColumnType.COLUMN
      : ResponsiveRowColumnType.ROW,
  children: [
    ResponsiveRowColumnItem(
      child: Container(width: 100, height: 100, color: Colors.red),
    ),
    ResponsiveRowColumnItem(
      child: Container(width: 100, height: 100, color: Colors.green),
    ),
  ],
);
```

---

#### ➤ **flutter\_screenutil** (alternative)

```dart
import 'package:flutter_screenutil/flutter_screenutil.dart';

ScreenUtilInit(
  designSize: Size(360, 690),
  builder: () => MaterialApp(
    home: MyHomePage(),
  ),
);
```

Use like:

```dart
Text('Hello', style: TextStyle(fontSize: 18.sp)); // 18 scaled
```

---

## ✅ Summary Table

| Feature               | Purpose                               | Example                             |
| --------------------- | ------------------------------------- | ----------------------------------- |
| MediaQuery            | Get screen dimensions and orientation | `MediaQuery.of(context).size.width` |
| LayoutBuilder         | Respond to widget-level constraints   | `if (constraints.maxWidth > 600)`   |
| FittedBox             | Scale child to fit within bounds      | `FittedBox(child: Text(...))`       |
| responsive\_framework | Build for mobile, tablet, desktop     | `ResponsiveWrapper.builder(...)`    |

---
 