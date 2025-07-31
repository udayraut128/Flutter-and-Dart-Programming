## 🟦 **Topic 21: Memory Management & Garbage Collection in Dart**

Dart handles memory management **automatically** using a **garbage collector**. However, understanding how memory is allocated, used, and collected helps write more **efficient and optimized programs**.

---

### 🔹 21.1: **Stack and Heap**

#### ✅ Stack

* **Stores:** Local variables, function calls
* **Fast access**
* Automatically deallocated when function ends
* Follows **Last In First Out (LIFO)**

#### ✅ Heap

* **Stores:** Objects, closures, long-living variables
* Managed dynamically
* Slower but flexible

> Dart uses the **stack** for managing function calls and the **heap** for objects.

---

### 🔹 Example: Stack vs Heap

```dart
void main() {
  int x = 10; // Stored in stack
  var person = Person(); // Person object stored in heap
}

class Person {
  String name = 'John';
}
```

* `x` is a primitive → stack.
* `person` is an object → reference on stack, actual object on heap.

---

### 🔹 21.2: **Automatic Garbage Collection**

Dart uses **mark-and-sweep garbage collection**:

1. **Mark**: Finds objects still in use.
2. **Sweep**: Deletes objects no longer referenced.

> You don’t need to manually free memory in Dart. When no variable refers to an object, it becomes **garbage** and Dart cleans it up.

#### Example:

```dart
void main() {
  var person = Person('Alice');
  person = null; // Person is now garbage
}
```

---

### 🔹 21.3: **Object Lifecycle**

Object’s lifecycle:

1. **Creation** → using `new` or constructor.
2. **Use** → accessed or modified in the program.
3. **Unreachable** → no references remain.
4. **Collected** → Dart deletes it during GC.

---

### 🧠 Tips for Efficient Memory Management

✅ Use `const` for immutable objects — they're cached.
✅ Dispose unused controllers (`TextEditingController`, `StreamController`).
✅ Avoid memory leaks by breaking circular references.
✅ Use `final` where values won’t change.
✅ Don’t retain large data in memory unnecessarily.

---

### 🔎 Debugging Tools

In Flutter:

* **DevTools Memory tab** shows heap usage, GC, memory leaks, etc.
* Use `debugPrint()` to trace memory-heavy objects.

---

### Summary Table:

| Concept            | Description                                     |
| ------------------ | ----------------------------------------------- |
| Stack              | Fast memory for local variables, function calls |
| Heap               | Dynamic memory for objects and long-living data |
| Garbage Collection | Automatic removal of unused memory              |
| Object Lifecycle   | Create → Use → Unreachable → Collected          |
| Tools              | Flutter DevTools (Memory tab), debugPrint       |

---

 