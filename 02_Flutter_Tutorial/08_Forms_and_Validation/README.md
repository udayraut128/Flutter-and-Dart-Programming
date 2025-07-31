# 📝 Flutter Forms and Validation

---

## 1. **TextFormField**

### ✅ What is TextFormField?

* A widget for getting text input from the user.
* Unlike `TextField`, it integrates with the `Form` widget and supports validation.
* Provides features like validators, saving, resetting, and more.

---

### 🔧 Basic Usage:

```dart
TextFormField(
  decoration: InputDecoration(
    labelText: 'Enter your name',
    border: OutlineInputBorder(),
  ),
)
```

---

### 🧪 Example 1: TextFormField with basic validation

```dart
TextFormField(
  decoration: InputDecoration(labelText: 'Email'),
  validator: (value) {
    if (value == null || value.isEmpty) {
      return 'Please enter your email';
    }
    if (!value.contains('@')) {
      return 'Please enter a valid email';
    }
    return null;
  },
),
```

---

## 2. **Form Widget**

### ✅ What is Form?

* A container for grouping multiple form fields (`TextFormField`).
* Manages the state of the form.
* Allows you to validate, save, or reset all fields collectively.

---

### 🔧 How to use Form?

* Wrap your input fields inside `Form`.
* Associate a `GlobalKey<FormState>` to the form for managing its state.

```dart
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(...),
      ElevatedButton(
        onPressed: () {
          if (_formKey.currentState!.validate()) {
            // Form is valid
          }
        },
        child: Text('Submit'),
      )
    ],
  ),
);
```

---

### 🧪 Example 2: Complete form with multiple fields

```dart
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(
        decoration: InputDecoration(labelText: 'Username'),
        validator: (value) {
          if (value == null || value.isEmpty) {
            return 'Username is required';
          }
          return null;
        },
      ),
      TextFormField(
        decoration: InputDecoration(labelText: 'Password'),
        obscureText: true,
        validator: (value) {
          if (value == null || value.length < 6) {
            return 'Password must be at least 6 characters';
          }
          return null;
        },
      ),
      ElevatedButton(
        onPressed: () {
          if (_formKey.currentState!.validate()) {
            // All validations passed
            print('Form is valid');
          }
        },
        child: Text('Login'),
      ),
    ],
  ),
);
```

---

## 3. **Validators**

### ✅ What are Validators?

* Functions that return `null` if the input is valid, or a **String error message** if invalid.
* Common validators include checking for empty fields, length, patterns (like email), numbers, etc.

---

### 🔧 Common Validator Examples:

```dart
String? emailValidator(String? value) {
  if (value == null || value.isEmpty) {
    return 'Email is required';
  }
  if (!RegExp(r'^[^@]+@[^@]+\.[^@]+').hasMatch(value)) {
    return 'Enter a valid email';
  }
  return null;
}
```

---

### 🧪 Example 3: Using multiple validators with `FormFieldValidator`

You can combine validators like:

```dart
final emailValidator = (String? value) {
  if (value == null || value.isEmpty) return 'Email required';
  if (!value.contains('@')) return 'Invalid email';
  return null;
};
```

---

## 4. **GlobalKey**

### ✅ What is GlobalKey?

* A unique identifier for widgets in the widget tree.
* Allows you to **access and manipulate the state** of a widget (like a Form).
* Essential for calling methods like `validate()`, `save()`, and `reset()` on `FormState`.

---

### 🔧 How to create and use GlobalKey for Form?

```dart
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: ...,
);

// Later in code
if (_formKey.currentState!.validate()) {
  // Proceed
}
```

---

### 🧪 Example 4: Resetting form with GlobalKey

```dart
ElevatedButton(
  onPressed: () {
    _formKey.currentState!.reset();
  },
  child: Text('Reset'),
),
```

---

# Summary Table

| Concept       | Purpose                                      | Usage Example                                       |
| ------------- | -------------------------------------------- | --------------------------------------------------- |
| TextFormField | Input field with validation support          | `TextFormField(validator: ...)`                     |
| Form          | Container to group form fields               | `Form(key: _formKey, child: ...)`                   |
| Validators    | Functions to validate input and return error | `validator: (val) => val!.isEmpty ? 'Error' : null` |
| GlobalKey     | Unique key to access widget state            | `GlobalKey<FormState> _formKey = GlobalKey();`      |

---


