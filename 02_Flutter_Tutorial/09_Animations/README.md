 # 🎬 Animations in Flutter

Flutter offers two main ways to create animations:

* **Implicit Animations:** Easy to use, less code, ideal for simple animations.
* **Explicit Animations:** More control and flexibility, requires animation controllers.

---

## 1. **Implicit Animations**

### ✅ What are Implicit Animations?

* Widgets that animate changes to their properties automatically when those properties change.
* You just change a property and Flutter animates the transition smoothly.
* No need to manage animation controllers or animation lifecycle manually.

### 🔧 Common Implicit Animation Widgets

* `AnimatedContainer`
* `AnimatedOpacity`
* `AnimatedPadding`
* `AnimatedAlign`
* `AnimatedCrossFade`
* `AnimatedDefaultTextStyle`

---

### 🧪 Example 1: AnimatedContainer

```dart
class AnimatedContainerExample extends StatefulWidget {
  @override
  _AnimatedContainerExampleState createState() => _AnimatedContainerExampleState();
}

class _AnimatedContainerExampleState extends State<AnimatedContainerExample> {
  double _width = 100;
  double _height = 100;
  Color _color = Colors.blue;

  void _changeProperties() {
    setState(() {
      _width = _width == 100 ? 200 : 100;
      _height = _height == 100 ? 200 : 100;
      _color = _color == Colors.blue ? Colors.red : Colors.blue;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        AnimatedContainer(
          width: _width,
          height: _height,
          color: _color,
          duration: Duration(seconds: 1),
          curve: Curves.easeInOut,
        ),
        ElevatedButton(
          onPressed: _changeProperties,
          child: Text('Animate Container'),
        ),
      ],
    );
  }
}
```

---

### 🧪 Example 2: AnimatedOpacity

```dart
class AnimatedOpacityExample extends StatefulWidget {
  @override
  _AnimatedOpacityExampleState createState() => _AnimatedOpacityExampleState();
}

class _AnimatedOpacityExampleState extends State<AnimatedOpacityExample> {
  double _opacity = 1.0;

  void _toggleOpacity() {
    setState(() {
      _opacity = _opacity == 1.0 ? 0.0 : 1.0;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        AnimatedOpacity(
          opacity: _opacity,
          duration: Duration(seconds: 1),
          child: Container(
            width: 200,
            height: 200,
            color: Colors.green,
          ),
        ),
        ElevatedButton(
          onPressed: _toggleOpacity,
          child: Text('Toggle Opacity'),
        ),
      ],
    );
  }
}
```

---

### 🧪 Example 3: AnimatedPadding

```dart
class AnimatedPaddingExample extends StatefulWidget {
  @override
  _AnimatedPaddingExampleState createState() => _AnimatedPaddingExampleState();
}

class _AnimatedPaddingExampleState extends State<AnimatedPaddingExample> {
  double _padding = 10;

  void _changePadding() {
    setState(() {
      _padding = _padding == 10 ? 50 : 10;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        AnimatedPadding(
          padding: EdgeInsets.all(_padding),
          duration: Duration(seconds: 1),
          child: Container(
            color: Colors.orange,
            width: 100,
            height: 100,
          ),
        ),
        ElevatedButton(
          onPressed: _changePadding,
          child: Text('Animate Padding'),
        ),
      ],
    );
  }
}
```

---

## 2. **Explicit Animations**

### ✅ What are Explicit Animations?

* You manage the animation **controller** and **animation objects**.
* Full control over animation timing, curves, and lifecycle.
* Good for complex animations or custom effects.

### 🔧 How to implement?

* Use `AnimationController` for controlling animation duration and lifecycle.
* Use `Animation<T>` for interpolation.
* Use `AnimatedBuilder` or listen to the animation and rebuild widgets.

---

### 🧪 Example 4: Basic Explicit Animation with AnimatedBuilder

```dart
class ExplicitAnimationExample extends StatefulWidget {
  @override
  _ExplicitAnimationExampleState createState() => _ExplicitAnimationExampleState();
}

class _ExplicitAnimationExampleState extends State<ExplicitAnimationExample> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      vsync: this,
      duration: Duration(seconds: 2),
    );

    _animation = Tween<double>(begin: 0, end: 300).animate(
      CurvedAnimation(parent: _controller, curve: Curves.easeInOut),
    );

    _controller.repeat(reverse: true);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animation,
      builder: (context, child) {
        return Container(
          width: _animation.value,
          height: _animation.value,
          color: Colors.purple,
        );
      },
    );
  }
}
```

---

### 🧪 Example 5: Explicit Animation with FadeTransition

```dart
class FadeTransitionExample extends StatefulWidget {
  @override
  _FadeTransitionExampleState createState() => _FadeTransitionExampleState();
}

class _FadeTransitionExampleState extends State<FadeTransitionExample> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _fadeAnimation;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      duration: Duration(seconds: 3),
      vsync: this,
    );

    _fadeAnimation = Tween<double>(begin: 0, end: 1).animate(_controller);

    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return FadeTransition(
      opacity: _fadeAnimation,
      child: Container(
        width: 200,
        height: 200,
        color: Colors.blue,
      ),
    );
  }
}
```

---

### 🧪 Example 6: SizeTransition with AnimationController

```dart
class SizeTransitionExample extends StatefulWidget {
  @override
  _SizeTransitionExampleState createState() => _SizeTransitionExampleState();
}

class _SizeTransitionExampleState extends State<SizeTransitionExample> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _sizeAnimation;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      vsync: this,
      duration: Duration(seconds: 2),
    )..repeat(reverse: true);

    _sizeAnimation = Tween<double>(begin: 0.5, end: 1).animate(_controller);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: SizeTransition(
        sizeFactor: _sizeAnimation,
        axis: Axis.horizontal,
        axisAlignment: -1,
        child: Container(
          width: 200,
          height: 200,
          color: Colors.teal,
        ),
      ),
    );
  }
}
```

---

# Summary Table

| Animation Type     | Description                              | Example Widgets                                     |
| ------------------ | ---------------------------------------- | --------------------------------------------------- |
| Implicit Animation | Auto-animate on property changes         | AnimatedContainer, AnimatedOpacity, AnimatedPadding |
| Explicit Animation | Manual control using AnimationController | AnimatedBuilder, FadeTransition, SizeTransition     |

---
 

# 🎨 Flutter Animation Deep Dive

---

## 1. **AnimationController**

### ✅ What is AnimationController?

* A special animation object that **controls the animation’s duration, playback, and state**.
* It generates a new value whenever the device’s screen refreshes (usually 60 times per second).
* You **drive the animation** by starting, stopping, repeating, or reversing the controller.
* Requires a `TickerProvider` (usually your `State` class with `SingleTickerProviderStateMixin`).

---

### 🔧 Basic Usage

```dart
class MyAnimatedWidget extends StatefulWidget {
  @override
  _MyAnimatedWidgetState createState() => _MyAnimatedWidgetState();
}

class _MyAnimatedWidgetState extends State<MyAnimatedWidget> with SingleTickerProviderStateMixin {
  late AnimationController _controller;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,  // Required for efficiency, provides ticker for animation frames
    );

    _controller.forward();  // Start animation
  }

  @override
  void dispose() {
    _controller.dispose();  // Release resources
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      width: 100 * _controller.value,
      height: 100,
      color: Colors.blue,
    );
  }
}
```

---

## 2. **Tween & Curves**

### ✅ What is Tween?

* Short for **“in-between”**, it defines how to interpolate between a **begin** and **end** value over time.
* Works with `AnimationController` to produce intermediate values.
* Common tweens: `Tween<double>`, `ColorTween`, `SizeTween`, etc.

---

### ✅ What are Curves?

* Defines the **rate of change** during the animation.
* Control speed and easing: linear, easeIn, easeOut, bounce, elastic, etc.
* Use with `CurvedAnimation` to apply curve to an animation.

---

### 🔧 Tween + Curves Example

```dart
class TweenCurvesExample extends StatefulWidget {
  @override
  _TweenCurvesExampleState createState() => _TweenCurvesExampleState();
}

class _TweenCurvesExampleState extends State<TweenCurvesExample> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(duration: Duration(seconds: 3), vsync: this);

    _animation = Tween<double>(begin: 0, end: 300).animate(
      CurvedAnimation(
        parent: _controller,
        curve: Curves.easeInOutBack, // smooth acceleration and deceleration
      ),
    );

    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animation,
      builder: (context, child) {
        return Container(
          width: _animation.value,
          height: _animation.value,
          color: Colors.orange,
        );
      },
    );
  }
}
```

---

## 3. **Hero Animations**

### ✅ What is Hero Animation?

* Used for **shared element transitions** between screens.
* Animates a widget from one screen to another seamlessly.
* Requires wrapping widgets on both screens with `Hero` widget sharing the same `tag`.

---

### 🔧 Basic Hero Animation Example

```dart
// Screen 1
GestureDetector(
  onTap: () => Navigator.push(context, MaterialPageRoute(builder: (_) => DetailScreen())),
  child: Hero(
    tag: 'hero-image',
    child: Image.network('https://picsum.photos/200'),
  ),
);

// Screen 2 (DetailScreen)
Hero(
  tag: 'hero-image',
  child: Image.network('https://picsum.photos/400'),
),
```

---

### 🧪 Example 2: Hero Animation with Text

```dart
// Screen 1
Hero(
  tag: 'hero-text',
  child: Material(
    color: Colors.transparent,
    child: Text('Hello Hero!', style: TextStyle(fontSize: 24)),
  ),
);

// Screen 2
Hero(
  tag: 'hero-text',
  child: Material(
    color: Colors.transparent,
    child: Text('Hello Hero!', style: TextStyle(fontSize: 48)),
  ),
);
```

---

## 4. **Custom Animations**

### ✅ What is Custom Animation?

* Using `AnimationController`, `Tween`, and custom `AnimatedWidget` or `AnimatedBuilder` to create **complex, tailored animations**.
* You can animate any widget property: size, position, rotation, color, opacity, etc.

---

### 🔧 Example 3: Rotation Animation using AnimatedBuilder

```dart
class RotationAnimation extends StatefulWidget {
  @override
  _RotationAnimationState createState() => _RotationAnimationState();
}

class _RotationAnimationState extends State<RotationAnimation> with SingleTickerProviderStateMixin {
  late AnimationController _controller;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      duration: Duration(seconds: 4),
      vsync: this,
    )..repeat();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _controller,
      child: Icon(Icons.refresh, size: 100),
      builder: (context, child) {
        return Transform.rotate(
          angle: _controller.value * 2 * 3.14159, // full rotation
          child: child,
        );
      },
    );
  }
}
```

---

### 🧪 Example 4: Slide Animation (Move widget from left to right)

```dart
class SlideAnimationExample extends StatefulWidget {
  @override
  _SlideAnimationExampleState createState() => _SlideAnimationExampleState();
}

class _SlideAnimationExampleState extends State<SlideAnimationExample> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<Offset> _offsetAnimation;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(duration: Duration(seconds: 2), vsync: this);

    _offsetAnimation = Tween<Offset>(begin: Offset(-1, 0), end: Offset(1, 0)).animate(
      CurvedAnimation(parent: _controller, curve: Curves.easeInOut),
    );

    _controller.repeat(reverse: true);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return SlideTransition(
      position: _offsetAnimation,
      child: Container(
        width: 100,
        height: 100,
        color: Colors.green,
      ),
    );
  }
}
```

---

# Summary Table

| Concept             | Purpose                          | Example Widgets / Classes                         |
| ------------------- | -------------------------------- | ------------------------------------------------- |
| AnimationController | Control animation timing & state | `AnimationController`                             |
| Tween               | Define value interpolation       | `Tween<double>`, `ColorTween`                     |
| Curves              | Smooth or custom easing curves   | `Curves.easeInOut`, `Curves.bounce`               |
| Hero Animation      | Shared element transitions       | `Hero`                                            |
| Custom Animations   | Complex tailored animations      | `AnimatedBuilder`, `Transform`, `SlideTransition` |

---
 