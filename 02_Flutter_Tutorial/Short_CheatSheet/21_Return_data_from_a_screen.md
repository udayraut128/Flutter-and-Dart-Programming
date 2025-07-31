### 🔁 **Return Data from a Screen in Flutter** – Full Explanation

When navigating in Flutter, not only can you **send data to a screen**, but you can also **return data** back to the previous screen — useful for things like selections, confirmations, or input results.

---

## ✅ Use Cases

* Selecting an item from a list and returning the selected item
* Returning a result (e.g., success/failure) from a form
* Getting confirmation from a user (like Yes/No)

---

## 🚀 Basic Flow

1. Navigate to a new screen using `Navigator.push`
2. Wait for a result using `await`
3. Return data from the second screen using `Navigator.pop`

---

## 📦 Full Example

### 🧱 Step 1: First Screen (Calls Second Screen and Receives Data)

```dart
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('First Screen')),
      body: Center(
        child: ElevatedButton(
          child: Text('Pick a fruit'),
          onPressed: () async {
            // Navigate to second screen and wait for result
            final result = await Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );

            // Use the result
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(content: Text('You picked: $result')),
            );
          },
        ),
      ),
    );
  }
}
```

---

### 🧱 Step 2: Second Screen (Returns Data)

```dart
class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Choose a Fruit')),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          ElevatedButton(
            child: Text('Apple'),
            onPressed: () {
              Navigator.pop(context, 'Apple'); // Return data
            },
          ),
          ElevatedButton(
            child: Text('Banana'),
            onPressed: () {
              Navigator.pop(context, 'Banana'); // Return data
            },
          ),
        ],
      ),
    );
  }
}
```

---

## 🧠 Explanation

| Method                         | Description                                                |
| ------------------------------ | ---------------------------------------------------------- |
| `Navigator.push()`             | Opens a new screen and **waits** for a result              |
| `await`                        | Waits until the second screen is popped                    |
| `Navigator.pop(context, data)` | Closes the screen and **returns data** to the previous one |

---

## 📄 Return Custom Object

You can return not just a string or int, but any object.

```dart
// On second screen
class User {
  final String name;
  final int age;

  User(this.name, this.age);
}

// Inside a button
Navigator.pop(context, User("John", 25));

// On first screen
final result = await Navigator.push(context, ...);
print(result.name);
```

---

## 🔍 Handling Null Result (User Pressed Back Button)

```dart
final result = await Navigator.push(...);
if (result != null) {
  print('User selected: $result');
} else {
  print('No selection made.');
}
```

---

## 🧪 Test This:

✅ Tap a button
✅ Choose an option
✅ See a SnackBar with returned result

---

## 🎯 Summary

| Task                           | Code Example                               |
| ------------------------------ | ------------------------------------------ |
| Navigate and wait for data     | `final result = await Navigator.push(...)` |
| Return data from second screen | `Navigator.pop(context, data)`             |
| Handle null result             | `if (result != null)`                      |

---

