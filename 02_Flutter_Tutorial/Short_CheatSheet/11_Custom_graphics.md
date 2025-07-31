
---

# 🎨 Custom Graphics in Flutter → `Use Custom Fragment Shaders`

---

## 📌 What are Fragment Shaders?

A **fragment shader** is a small program that runs on the GPU and determines the **color of each pixel** on the screen. They are widely used in game development, animation, special effects, and advanced rendering techniques.

In Flutter, you can now write custom fragment shaders using **`FragmentProgram`** with the **Impeller rendering engine** (enabled by default on modern Flutter versions).

---

## 🚀 Why Use Custom Fragment Shaders in Flutter?

| Feature                | Benefit                                     |
| ---------------------- | ------------------------------------------- |
| 🎇 Pixel-level control | Create glow, blur, color effects            |
| 🎮 GPU accelerated     | Fast & smooth rendering                     |
| 🧩 Reusable effects    | Apply shaders to multiple widgets or scenes |
| 🔥 Advanced visuals    | Make your UI/game/animation look awesome    |

---

## 🧱 Requirements

✅ Flutter 3.10+
✅ Dart SDK 3.0+
✅ Impeller (default engine on iOS and enabled on Android)
✅ `.frag` shader files written in GLSL

---

## 🧪 Example: Using a Custom Fragment Shader

---

### Step 1: Create a `.frag` Shader File

Create a folder called `shaders/` in your root directory and add a `.frag` file.

```glsl
// shaders/invert.frag
// This inverts the color of each pixel

precision mediump float;

uniform sampler2D texture;
varying vec2 v_texCoord;

void main() {
  vec4 color = texture2D(texture, v_texCoord);
  gl_FragColor = vec4(1.0 - color.rgb, color.a);
}
```

---

### Step 2: Declare Shader in `pubspec.yaml`

```yaml
flutter:
  shaders:
    - shaders/invert.frag
```

---

### Step 3: Use Shader in Dart Code

```dart
import 'dart:ui' as ui;
import 'package:flutter/material.dart';

class ShaderWidget extends StatefulWidget {
  const ShaderWidget({Key? key}) : super(key: key);

  @override
  State<ShaderWidget> createState() => _ShaderWidgetState();
}

class _ShaderWidgetState extends State<ShaderWidget> {
  late Future<ui.FragmentProgram> _shader;

  @override
  void initState() {
    super.initState();
    _shader = ui.FragmentProgram.fromAsset('shaders/invert.frag');
  }

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<ui.FragmentProgram>(
      future: _shader,
      builder: (context, snapshot) {
        if (!snapshot.hasData) return const CircularProgressIndicator();

        final shader = snapshot.data!.fragmentShader();

        return CustomPaint(
          painter: ShaderPainter(shader),
          size: const Size(double.infinity, double.infinity),
        );
      },
    );
  }
}

class ShaderPainter extends CustomPainter {
  final ui.FragmentShader shader;

  ShaderPainter(this.shader);

  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()..shader = shader;

    // Draw full canvas with the shader effect
    canvas.drawRect(Offset.zero & size, paint);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}
```

---

## 🛠 Shader Limitations & Notes

* Only available with **Impeller engine**
* Cannot run on **Web** as of now (no WebGL support)
* Requires **basic GLSL knowledge**
* Uses a different coordinate system (0–1 for texture mapping)

---

## 🧠 When to Use Shaders in Flutter

| Use Case               | Example                         |
| ---------------------- | ------------------------------- |
| 🎞 Image filtering     | Invert, blur, sepia             |
| 💡 Lighting effects    | Shadows, glow, neon             |
| 🔥 Fire/water effects  | Animated shaders                |
| 🎮 Game graphics       | Real-time game effects          |
| 🖼️ Custom backgrounds | Procedural art, waves, fractals |

---

## 📚 Resources

* 📖 [Flutter Shader Support Docs](https://docs.flutter.dev/ui/advanced/shaders)
* 🎮 [GLSL Sandbox](https://glslsandbox.com/) – for trying shader code online
* 🔤 [ShaderToy](https://www.shadertoy.com/) – community-shared GLSL effects
* 🛠 [Impeller Engine Details](https://docs.flutter.dev/perf/impeller)

---

## ✅ Summary

| Topic            | Description                                                    |
| ---------------- | -------------------------------------------------------------- |
| Fragment Shaders | GPU programs that paint each pixel                             |
| How to Use       | Write `.frag` GLSL → add in `pubspec.yaml` → `FragmentProgram` |
| Key Benefits     | Fast, pixel-level visual control                               |
| Limitations      | Not supported on Web, needs Impeller                           |

---
 