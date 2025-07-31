

---

# 🎯 Flutter User Interaction: Snackbar, Actions & Keyboard Focus

This guide explains:

1. ✅ Display a Snackbar
2. ⌨️ Implement Actions and Shortcuts
3. 🎯 Manage Keyboard Focus

---

## ✅ 1. Display a Snackbar

### 🔹 What is a Snackbar?

A **Snackbar** provides lightweight feedback about an operation. It briefly displays at the bottom of the screen.

---

### ✨ Basic Example:

```dart
ScaffoldMessenger.of(context).showSnackBar(
  SnackBar(
    content: Text('Item added to cart!'),
  ),
);
```

You must use `ScaffoldMessenger.of(context)` (NOT `Scaffold.of()` anymore).

---

### 🔹 Snackbar with Action

```dart
ScaffoldMessenger.of(context).showSnackBar(
  SnackBar(
    content: Text('Undo delete?'),
    action: SnackBarAction(
      label: 'Undo',
      onPressed: () {
        // Perform undo action
      },
    ),
  ),
);
```

---

### 🔹 Customize Snackbar

```dart
SnackBar(
  content: Text('Custom styled snackbar'),
  backgroundColor: Colors.blueGrey,
  duration: Duration(seconds: 3),
  behavior: SnackBarBehavior.floating,
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
)
```

---

## ⌨️ 2. Implement Actions and Shortcuts

Flutter supports **keyboard shortcuts and actions** using `Actions`, `Shortcuts`, and `Intent`. These are helpful for:

* Accessibility
* Keyboard navigation (especially on desktop/web)
* Advanced UI control

---

### ✨ Step-by-step Example

Let’s bind the **Enter key** to show a snackbar.

---

### 🔹 1. Define a Custom Intent

```dart
class ShowSnackbarIntent extends Intent {
  const ShowSnackbarIntent();
}
```

---

### 🔹 2. Define an Action

```dart
class ShowSnackbarAction extends Action<ShowSnackbarIntent> {
  final BuildContext context;

  ShowSnackbarAction(this.context);

  @override
  void invoke(covariant ShowSnackbarIntent intent) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text('Shortcut Triggered!')),
    );
  }
}
```

---

### 🔹 3. Use `Actions` and `Shortcuts` Widget

```dart
Shortcuts(
  shortcuts: {
    LogicalKeySet(LogicalKeyboardKey.enter): ShowSnackbarIntent(),
  },
  child: Actions(
    actions: {
      ShowSnackbarIntent: ShowSnackbarAction(context),
    },
    child: Focus(
      autofocus: true,
      child: Center(child: Text('Press Enter to show Snackbar')),
    ),
  ),
)
```

---

## 🎯 3. Manage Keyboard Focus

To manage keyboard focus between fields or widgets, Flutter provides:

### Widgets:

* `Focus`
* `FocusNode`
* `FocusScope`

---

### 🔹 1. Basic Focus Control Between Two TextFields

```dart
FocusNode _focusNode1 = FocusNode();
FocusNode _focusNode2 = FocusNode();
```

```dart
TextField(
  focusNode: _focusNode1,
  decoration: InputDecoration(labelText: 'First Field'),
),

TextField(
  focusNode: _focusNode2,
  decoration: InputDecoration(labelText: 'Second Field'),
),

ElevatedButton(
  onPressed: () {
    FocusScope.of(context).requestFocus(_focusNode2); // Move to second field
  },
  child: Text('Focus Second Field'),
)
```

---

### 🔹 2. Unfocus (Hide Keyboard)

```dart
FocusScope.of(context).unfocus(); // Removes focus from all
```

---

### 🔹 3. Detect Keyboard Events

```dart
RawKeyboardListener(
  focusNode: FocusNode(),
  onKey: (RawKeyEvent event) {
    if (event.isKeyPressed(LogicalKeyboardKey.enter)) {
      print("Enter key pressed");
    }
  },
  child: TextField(),
)
```

---

## 📌 Summary Table

| Feature          | Key Classes / Methods                  | Purpose                       |
| ---------------- | -------------------------------------- | ----------------------------- |
| Snackbar         | `SnackBar`, `ScaffoldMessenger`        | Show brief UI messages        |
| Snackbar action  | `SnackBarAction`                       | Add "Undo", "Retry", etc.     |
| Shortcuts        | `Shortcuts`, `LogicalKeySet`, `Intent` | Map keyboard keys             |
| Actions          | `Actions`, `invoke()`                  | Define logic on shortcut      |
| Focus management | `FocusNode`, `FocusScope`, `unfocus()` | Programmatic keyboard control |

---

## ✅ Best Practices

* Use `ScaffoldMessenger` over `Scaffold.of` for snackbars.
* Use `Focus` and `Shortcuts` when building **desktop-friendly** or **accessibility-aware** apps.
* Combine `FocusScope.of(context).requestFocus()` with validation for better UX in forms.

---
 