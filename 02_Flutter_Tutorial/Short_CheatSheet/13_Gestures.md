
---

# 🤲 Flutter Gestures – Full Guide

Flutter provides a powerful gesture system that enables you to build highly interactive UIs by responding to **taps, drags, swipes, long presses**, and other touch interactions.

---

## 🔹 1. Introduction to Gestures in Flutter

In Flutter:

* **Widgets do not handle gestures by default.**
* You wrap widgets with **gesture-handling widgets** like `GestureDetector`, `InkWell`, or `Dismissible`.

Flutter gestures are part of the **gesture arena**:

* Multiple gesture detectors may be listening to the same pointer.
* The system determines which one wins based on gesture type and priority.

### 📌 Common Gestures Supported:

| Gesture                  | Widget Used                      |
| ------------------------ | -------------------------------- |
| Tap                      | `GestureDetector`, `InkWell`     |
| Double Tap               | `GestureDetector`                |
| Long Press               | `GestureDetector`                |
| Vertical/Horizontal Drag | `GestureDetector`, `Dismissible` |
| Scale (Pinch Zoom)       | `GestureDetector`                |

---

## 🔹 2. Handle Taps with `GestureDetector`

### ✅ Example: Tap, Double Tap, Long Press

```dart
GestureDetector(
  onTap: () => print('Tapped!'),
  onDoubleTap: () => print('Double Tapped!'),
  onLongPress: () => print('Long Pressed!'),
  child: Container(
    padding: EdgeInsets.all(20),
    color: Colors.blue,
    child: Text("Tap Me", style: TextStyle(color: Colors.white)),
  ),
)
```

### 📝 Output

* Tap once → `Tapped!`
* Double tap quickly → `Double Tapped!`
* Hold for a moment → `Long Pressed!`

---

## 🔹 3. Drag an Object Outside the App (Using `Draggable` and `DragTarget`)

Dragging across apps isn't natively supported in Flutter, but **within the app**, you can use `Draggable`.

```dart
Draggable<String>(
  data: "Flutter",
  feedback: Material(
    child: Container(
      color: Colors.red,
      padding: EdgeInsets.all(10),
      child: Text("Dragging"),
    ),
  ),
  child: Container(
    color: Colors.green,
    padding: EdgeInsets.all(10),
    child: Text("Drag Me"),
  ),
)
```

### Use with `DragTarget`:

```dart
DragTarget<String>(
  onAccept: (value) {
    print("Dropped: $value");
  },
  builder: (context, candidateData, rejectedData) {
    return Container(
      height: 100,
      width: 100,
      color: Colors.yellow,
      child: Center(child: Text("Drop Here")),
    );
  },
)
```

---

## 🔹 4. Drag a UI Element Within an App (e.g. Image or Container)

To move widgets **based on drag**, use `GestureDetector` with `onPanUpdate`.

### 🧲 Example:

```dart
class DraggableBox extends StatefulWidget {
  @override
  _DraggableBoxState createState() => _DraggableBoxState();
}

class _DraggableBoxState extends State<DraggableBox> {
  double x = 0;
  double y = 0;

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        Positioned(
          left: x,
          top: y,
          child: GestureDetector(
            onPanUpdate: (details) {
              setState(() {
                x += details.delta.dx;
                y += details.delta.dy;
              });
            },
            child: Container(
              width: 100,
              height: 100,
              color: Colors.red,
              child: Center(child: Text("Drag Me")),
            ),
          ),
        ),
      ],
    );
  }
}
```

🔁 `onPanUpdate` continuously tracks the drag, and the widget updates its position using `setState`.

---

## 🔹 5. Add Material Touch Ripples with `InkWell`

If you're following Material Design guidelines, use `InkWell` to provide **ripple feedback**.

### 🪄 Example:

```dart
InkWell(
  onTap: () {
    print("Tapped with ripple");
  },
  child: Container(
    padding: EdgeInsets.all(20),
    child: Text("Ripple Button"),
  ),
)
```

📌 Note: Must be used inside a `Material` widget for the ripple effect to appear properly.

```dart
Material(
  child: InkWell(...),
)
```

---

## 🔹 6. Implement Swipe to Dismiss with `Dismissible`

Swipe-to-dismiss allows items (e.g. in a List) to be removed by swiping.

### 🧹 Example: Dismiss List Items

```dart
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    final item = items[index];
    return Dismissible(
      key: Key(item),
      direction: DismissDirection.endToStart,
      onDismissed: (direction) {
        setState(() {
          items.removeAt(index);
        });
        ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(content: Text("$item dismissed")),
        );
      },
      background: Container(color: Colors.red),
      child: ListTile(title: Text(item)),
    );
  },
)
```

### 💡 Options:

* `DismissDirection.startToEnd` or `endToStart`
* Show delete icon or confirmation before deletion
* Customize background for visual feedback

---

## 📌 Summary Table

| Gesture Type         | Widget                         | Description                     |
| -------------------- | ------------------------------ | ------------------------------- |
| Tap / Long Press     | `GestureDetector`              | Basic tap handling              |
| Ripple Touch         | `InkWell`                      | Adds visual feedback (Material) |
| Drag (Any direction) | `GestureDetector`, `Draggable` | Move widget or drag data        |
| Swipe to Dismiss     | `Dismissible`                  | Remove item from list on swipe  |
| Custom Touch Logic   | `onPanUpdate`, `onScaleUpdate` | Handle drag, zoom, pan          |

---

## ✅ Best Practices

* Use `InkWell` for visual feedback with Material components.
* For simple gestures, `GestureDetector` is lightweight and flexible.
* Use `Dismissible` with lists, `Draggable` + `DragTarget` for drag-and-drop apps.
* Always test gesture interactions on **physical devices** for accurate feedback.

---
 