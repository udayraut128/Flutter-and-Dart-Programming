# 🔥 Flutter State Management: Basics and Intermediate Concepts

---

## 1. **`setState()`**

### ✅ What is `setState()`?

* The simplest way to manage state in Flutter.
* Used in **StatefulWidgets** to tell Flutter the state has changed and the UI should rebuild.
* Triggers a rebuild of the widget tree **below the StatefulWidget**.

---

### 🔧 How to use?

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  int counter = 0;

  void incrementCounter() {
    setState(() {
      counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Counter: $counter'),
        ElevatedButton(
          onPressed: incrementCounter,
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

---

### 🧪 Example 1: Toggle Button with `setState()`

```dart
bool isOn = false;

Switch(
  value: isOn,
  onChanged: (value) {
    setState(() {
      isOn = value;
    });
  },
);
```

---

### 🧪 Example 2: Simple TextField updating state

```dart
String inputText = '';

TextField(
  onChanged: (text) {
    setState(() {
      inputText = text;
    });
  },
),
Text('You typed: $inputText'),
```

---

## 2. **Lifting State Up**

### ✅ What is Lifting State Up?

* When multiple widgets need to share the **same piece of state**, the state is moved (lifted) **up** to the closest common ancestor.
* This allows both widgets to access and modify the shared state via callbacks and properties.

---

### 🔧 How to do it?

* Keep the state in the parent widget.
* Pass the state down as constructor parameters.
* Pass callbacks from the parent to children to update the state.

---

### 🧪 Example 3: Lifting State Up for Siblings

```dart
class ParentWidget extends StatefulWidget {
  @override
  _ParentWidgetState createState() => _ParentWidgetState();
}

class _ParentWidgetState extends State<ParentWidget> {
  String text = '';

  void updateText(String newText) {
    setState(() {
      text = newText;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        ChildInput(onTextChanged: updateText),
        ChildDisplay(text: text),
      ],
    );
  }
}

class ChildInput extends StatelessWidget {
  final Function(String) onTextChanged;

  ChildInput({required this.onTextChanged});

  @override
  Widget build(BuildContext context) {
    return TextField(
      onChanged: onTextChanged,
    );
  }
}

class ChildDisplay extends StatelessWidget {
  final String text;

  ChildDisplay({required this.text});

  @override
  Widget build(BuildContext context) {
    return Text('You typed: $text');
  }
}
```

---

## 3. **InheritedWidget**

### ✅ What is `InheritedWidget`?

* A low-level widget that **efficiently shares state down the widget tree**.
* Widgets can **subscribe** to `InheritedWidget` changes and rebuild only when the data changes.
* Useful for app-wide state or to avoid **prop drilling** (passing data through many widget levels).

---

### 🔧 How to use?

* Create a class extending `InheritedWidget`.
* Define a static `of(context)` method to easily access the data.
* Use `updateShouldNotify` to notify dependent widgets when data changes.

---

### 🧪 Example 4: Simple Counter with InheritedWidget

```dart
class CounterProvider extends InheritedWidget {
  final int counter;
  final Widget child;

  CounterProvider({required this.counter, required this.child}) : super(child: child);

  static CounterProvider? of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<CounterProvider>();
  }

  @override
  bool updateShouldNotify(CounterProvider oldWidget) {
    return oldWidget.counter != counter;
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int counter = 0;

  void increment() {
    setState(() {
      counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return CounterProvider(
      counter: counter,
      child: Scaffold(
        appBar: AppBar(title: Text("InheritedWidget Example")),
        body: Center(child: CounterDisplay()),
        floatingActionButton: FloatingActionButton(
          onPressed: increment,
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}

class CounterDisplay extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final counter = CounterProvider.of(context)?.counter ?? 0;
    return Text('Counter: $counter');
  }
}
```

---

### When to Use What?

| State Management  | Use Case                                      |
| ----------------- | --------------------------------------------- |
| `setState()`      | Simple state in one widget                    |
| Lifting State Up  | Sharing state between closely related widgets |
| `InheritedWidget` | Sharing state widely in widget subtree        |

---

## Summary Table:

| Concept           | Description                                    | Example Use Case                |
| ----------------- | ---------------------------------------------- | ------------------------------- |
| `setState()`      | Local, simple UI updates inside StatefulWidget | Button click updates UI         |
| Lifting State Up  | Pass state & callbacks up/down widget tree     | Two siblings sharing text input |
| `InheritedWidget` | Share data efficiently down many widget levels | Theme data, app-wide state      |

---

# 🚀 Flutter State Management: Provider, Riverpod, BLoC

---

## 1. **Provider**

### ✅ What is Provider?

* A simple, efficient **dependency injection** and state management solution built on top of `InheritedWidget`.
* Helps to **provide and consume data** anywhere in the widget tree.
* Very popular and officially recommended by Flutter team for many apps.

### 🔧 How to use Provider?

* Define a **ChangeNotifier** class to hold state.
* Use `ChangeNotifierProvider` to provide it to widget tree.
* Use `Consumer` or `Provider.of` to listen and rebuild widgets.

---

### 🧪 Example 1: Counter App using Provider

**Step 1: Define ChangeNotifier**

```dart
class CounterModel extends ChangeNotifier {
  int _count = 0;
  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}
```

**Step 2: Provide it in main**

```dart
void main() {
  runApp(
    ChangeNotifierProvider(
      create: (_) => CounterModel(),
      child: MyApp(),
    ),
  );
}
```

**Step 3: Use Consumer to listen**

```dart
class CounterText extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<CounterModel>(
      builder: (context, counter, _) => Text('Count: ${counter.count}'),
    );
  }
}
```

**Step 4: Update state**

```dart
ElevatedButton(
  onPressed: () => context.read<CounterModel>().increment(),
  child: Text('Increment'),
),
```

---

### 🧪 Example 2: Access Provider without Consumer

```dart
var counter = Provider.of<CounterModel>(context); // rebuilds on notifyListeners
var counterNoRebuild = Provider.of<CounterModel>(context, listen: false); // no rebuild
```

---

## 2. **Riverpod**

### ✅ What is Riverpod?

* A **modern rewrite** of Provider with better safety, testability, and flexibility.
* Does **not** rely on `InheritedWidget`.
* Provides **compile-time safety** and supports multiple providers, async, and more.

### 🔧 How to use Riverpod?

* Use **providers** defined globally.
* Use `ConsumerWidget` or `Consumer` to listen.

---

### 🧪 Example 3: Counter App with Riverpod

**Step 1: Define Provider**

```dart
final counterProvider = StateNotifierProvider<CounterNotifier, int>((ref) {
  return CounterNotifier();
});

class CounterNotifier extends StateNotifier<int> {
  CounterNotifier() : super(0);

  void increment() => state++;
}
```

**Step 2: Use `ConsumerWidget`**

```dart
class CounterText extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final count = ref.watch(counterProvider);
    return Text('Count: $count');
  }
}
```

**Step 3: Button to increment**

```dart
ElevatedButton(
  onPressed: () => ref.read(counterProvider.notifier).increment(),
  child: Text('Increment'),
),
```

---

### 🧪 Example 4: Async Data with Riverpod

```dart
final futureProvider = FutureProvider<String>((ref) async {
  await Future.delayed(Duration(seconds: 2));
  return 'Data Loaded';
});

class AsyncWidget extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final asyncValue = ref.watch(futureProvider);

    return asyncValue.when(
      data: (data) => Text(data),
      loading: () => CircularProgressIndicator(),
      error: (err, stack) => Text('Error: $err'),
    );
  }
}
```

---

## 3. **BLoC (Business Logic Component)**

### ✅ What is BLoC?

* A pattern to separate **business logic from UI** using **Streams** and **Sinks**.
* Helps in building **reactive apps**.
* Supported by `flutter_bloc` package.

### 🔧 How to use BLoC?

* Define a **Bloc class** with events and states.
* Provide Bloc to widget tree.
* Use `BlocBuilder` and `BlocListener` to react to state changes.

---

### 🧪 Example 5: Simple Counter Bloc

**Step 1: Define Events**

```dart
abstract class CounterEvent {}
class IncrementEvent extends CounterEvent {}
```

**Step 2: Define Bloc**

```dart
class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<IncrementEvent>((event, emit) => emit(state + 1));
  }
}
```

**Step 3: Provide Bloc**

```dart
void main() {
  runApp(
    BlocProvider(
      create: (_) => CounterBloc(),
      child: MyApp(),
    ),
  );
}
```

**Step 4: Use BlocBuilder**

```dart
BlocBuilder<CounterBloc, int>(
  builder: (context, count) {
    return Text('Count: $count');
  },
)
```

**Step 5: Add Event**

```dart
ElevatedButton(
  onPressed: () {
    context.read<CounterBloc>().add(IncrementEvent());
  },
  child: Text('Increment'),
)
```

---

### 🧪 Example 6: Bloc with States (Loading, Loaded)

```dart
abstract class DataState {}
class Loading extends DataState {}
class Loaded extends DataState {
  final String data;
  Loaded(this.data);
}

class DataBloc extends Bloc<DataEvent, DataState> {
  DataBloc() : super(Loading()) {
    on<LoadDataEvent>((event, emit) async {
      emit(Loading());
      await Future.delayed(Duration(seconds: 2));
      emit(Loaded('Fetched Data'));
    });
  }
}
```

---

## Summary Table

| State Management | Usage                  | Pros                                    | Cons                                   |
| ---------------- | ---------------------- | --------------------------------------- | -------------------------------------- |
| Provider         | Simple, widely used    | Easy to learn, integrates well          | Can get verbose for complex apps       |
| Riverpod         | Modern, safe, flexible | Compile-time safety, better testability | Newer, slightly steeper learning curve |
| BLoC             | Stream-based, robust   | Scalable, good separation of concerns   | More boilerplate, complex              |

---

# ⚡ Flutter State Management: GetX, MobX, Redux

---

## 1. **GetX**

### ✅ What is GetX?

* A **lightweight and powerful** state management, routing, and dependency injection package.
* Focuses on **simplicity and performance**.
* Uses **reactive programming** with observable variables (`Rx`).

### 🔧 Key Features:

* Simple reactive state management.
* Easy navigation without context.
* Dependency injection and service management.

---

### 🧪 Example 1: Simple Counter with GetX

```dart
import 'package:get/get.dart';

// Controller with observable variable
class CounterController extends GetxController {
  var count = 0.obs;

  void increment() {
    count++;
  }
}

// Usage in UI
class CounterPage extends StatelessWidget {
  final CounterController c = Get.put(CounterController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Obx(() => Text('Count: ${c.count}')),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: c.increment,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

---

### 🧪 Example 2: Navigation with GetX (No context needed)

```dart
ElevatedButton(
  onPressed: () => Get.to(SecondPage()),
  child: Text('Go to Second Page'),
);
```

Back navigation:

```dart
Get.back();
```

---

### 🧪 Example 3: Dependency Injection

```dart
class MyService extends GetxService {
  void fetchData() {
    print('Fetching data...');
  }
}

// Inject service
final service = Get.put(MyService());

// Use service anywhere
service.fetchData();
```

---

## 2. **MobX**

### ✅ What is MobX?

* A **reactive state management** library originally from the JavaScript world, available in Dart.
* Uses **observables**, **actions**, and **reactions** to manage state.
* Works with code generation for boilerplate reduction.

### 🔧 Key Concepts:

* `@observable`: Reactive variables.
* `@action`: Functions that modify state.
* `Observer`: Widget that rebuilds when observables change.

---

### 🧪 Example 4: Simple Counter with MobX

**Step 1: Define Store**

```dart
import 'package:mobx/mobx.dart';

part 'counter.g.dart';

class Counter = _Counter with _$Counter;

abstract class _Counter with Store {
  @observable
  int count = 0;

  @action
  void increment() {
    count++;
  }
}
```

Run build runner to generate code:

```bash
flutter pub run build_runner build
```

---

**Step 2: Use Store in UI**

```dart
final counter = Counter();

Observer(
  builder: (_) => Text('Count: ${counter.count}'),
),

ElevatedButton(
  onPressed: counter.increment,
  child: Text('Increment'),
),
```

---

### 🧪 Example 5: Reaction to state changes

```dart
reaction((_) => counter.count, (int count) {
  print('Counter changed to $count');
});
```

---

## 3. **Redux**

### ✅ What is Redux?

* A **predictable state container** inspired by the JavaScript Redux library.
* Uses a **single immutable state tree**.
* State is updated via **actions** and **reducers**.
* Good for large and complex apps.

### 🔧 Key Concepts:

* **State:** Single source of truth.
* **Actions:** Describe what happened.
* **Reducers:** Pure functions to update state.
* **Store:** Holds app state.

---

### 🧪 Example 6: Simple Counter with Redux

**Step 1: Define State**

```dart
class AppState {
  final int count;
  AppState(this.count);
}
```

---

**Step 2: Define Actions**

```dart
class IncrementAction {}
```

---

**Step 3: Define Reducer**

```dart
AppState counterReducer(AppState state, dynamic action) {
  if (action is IncrementAction) {
    return AppState(state.count + 1);
  }
  return state;
}
```

---

**Step 4: Create Store**

```dart
final store = Store<AppState>(counterReducer, initialState: AppState(0));
```

---

**Step 5: Connect Store with UI**

```dart
StoreProvider(
  store: store,
  child: StoreConnector<AppState, int>(
    converter: (store) => store.state.count,
    builder: (context, count) {
      return Text('Count: $count');
    },
  ),
);
```

Button to dispatch action:

```dart
StoreConnector<AppState, VoidCallback>(
  converter: (store) {
    return () => store.dispatch(IncrementAction());
  },
  builder: (context, callback) {
    return ElevatedButton(
      onPressed: callback,
      child: Text('Increment'),
    );
  },
);
```

---

## Summary Table

| Library | Description                        | Pros                                            | Cons                                   |
| ------- | ---------------------------------- | ----------------------------------------------- | -------------------------------------- |
| GetX    | Lightweight, reactive, easy to use | Simple syntax, no context needed for navigation | Can encourage overuse, less structure  |
| MobX    | Reactive programming with codegen  | Powerful, minimal boilerplate                   | Requires build\_runner setup           |
| Redux   | Predictable, single state tree     | Great for large apps, clear flow                | More boilerplate, steep learning curve |

---


