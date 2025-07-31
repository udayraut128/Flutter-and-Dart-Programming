# 📦 1. **Asset Management**

### ✅ What is it?

Flutter uses an `assets` directory to store static resources like images, fonts, and JSON files. These must be declared in `pubspec.yaml`.

---

### 🔧 Setup in `pubspec.yaml`

```yaml
flutter:
  assets:
    - assets/images/
```

### ✅ Example 1: Folder Structure

```
project/
└── assets/
    └── images/
        ├── logo.png
        └── banner.jpg
```

---

### ✅ Example 2: Using an Asset Image

```dart
Image.asset('assets/images/logo.png');
```

---

### ✅ Example 3: Load JSON from assets

```dart
String data = await rootBundle.loadString('assets/data/sample.json');
```

---

### ✅ Example 4: Add Custom Font (Bonus Example)

```yaml
flutter:
  fonts:
    - family: Roboto
      fonts:
        - asset: assets/fonts/Roboto-Regular.ttf
```

---

# 🌐 2. **Network & Local Images**

### ✅ a) **Local Images**

Use `Image.asset` to show images stored in your project.

#### 🧪 Example 1:

```dart
Image.asset('assets/images/profile.png', width: 100, height: 100);
```

---

### ✅ b) **Network Images**

Use `Image.network` to load from a URL.

#### 🧪 Example 2:

```dart
Image.network(
  'https://example.com/image.jpg',
  width: 200,
  height: 100,
  fit: BoxFit.cover,
);
```

---

### 🧪 Example 3: Network Image with Error Handling

```dart
Image.network(
  'https://wrong-url.com/image.jpg',
  errorBuilder: (context, error, stackTrace) =>
      Text('Image not found!'),
);
```

---

### 🧪 Example 4: Fade-in Network Image

```dart
FadeInImage.assetNetwork(
  placeholder: 'assets/images/loading.gif',
  image: 'https://example.com/image.jpg',
);
```

---

# 🎯 3. **Icon Widgets**

### ✅ What are Icon Widgets?

Flutter includes built-in icon sets like `Icons`, `CupertinoIcons`, or custom ones like from [FontAwesome](https://pub.dev/packages/font_awesome_flutter).

---

### ✅ Example 1: Using Built-in Icons

```dart
Icon(Icons.home, size: 40, color: Colors.blue);
```

---

### ✅ Example 2: Icon Button

```dart
IconButton(
  icon: Icon(Icons.search),
  onPressed: () {
    print("Search pressed");
  },
);
```

---

### ✅ Example 3: Cupertino Icon

```dart
import 'package:flutter/cupertino.dart';

Icon(CupertinoIcons.heart_fill, color: Colors.red, size: 32);
```

---

### ✅ Example 4: Font Awesome Icons

```yaml
dependencies:
  font_awesome_flutter: ^10.0.0
```

```dart
import 'package:font_awesome_flutter/font_awesome_flutter.dart';

Icon(FontAwesomeIcons.github);
```

---

## ✅ Summary Table

| Category          | Widget/Method                | Use-Case Example                               |
| ----------------- | ---------------------------- | ---------------------------------------------- |
| Asset Image       | `Image.asset()`              | `Image.asset('assets/logo.png')`               |
| Network Image     | `Image.network()`            | `Image.network('https://example.com/img.jpg')` |
| Fade Image        | `FadeInImage.assetNetwork()` | Smooth loading of network image                |
| Icon Widget       | `Icon(Icons.home)`           | Show a home icon                               |
| Icon Button       | `IconButton()`               | Icon that performs action on tap               |
| Font Awesome Icon | `FontAwesomeIcons.facebook`  | Use custom icon sets                           |

---

## 🎬 1. **Video Player in Flutter**

### ✅ What is it?

Flutter uses the `video_player` package to play videos from assets, file system, or network.

---

### 🔧 Setup in `pubspec.yaml`

```yaml
dependencies:
  video_player: ^2.7.0
```

Then run: `flutter pub get`

---

### ✅ Example 1: Play Network Video

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

class NetworkVideoExample extends StatefulWidget {
  @override
  _NetworkVideoExampleState createState() => _NetworkVideoExampleState();
}

class _NetworkVideoExampleState extends State<NetworkVideoExample> {
  late VideoPlayerController _controller;

  @override
  void initState() {
    super.initState();
    _controller = VideoPlayerController.network(
      'https://flutter.github.io/assets-for-api-docs/assets/videos/bee.mp4',
    )..initialize().then((_) {
        setState(() {});
        _controller.play();
      });
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return _controller.value.isInitialized
        ? AspectRatio(
            aspectRatio: _controller.value.aspectRatio,
            child: VideoPlayer(_controller),
          )
        : CircularProgressIndicator();
  }
}
```

---

### ✅ Example 2: Video from Assets

* Add file: `assets/videos/sample.mp4`
* Update `pubspec.yaml`:

```yaml
assets:
  - assets/videos/sample.mp4
```

* Use:

```dart
VideoPlayerController.asset('assets/videos/sample.mp4')
```

---

### ✅ Example 3: Pause/Play Button

```dart
FloatingActionButton(
  onPressed: () {
    setState(() {
      _controller.value.isPlaying ? _controller.pause() : _controller.play();
    });
  },
  child: Icon(
    _controller.value.isPlaying ? Icons.pause : Icons.play_arrow,
  ),
)
```

---

### ✅ Example 4: Loop Video

```dart
_controller.setLooping(true);
```

---

## 🎧 2. **Audio Player in Flutter**

### ✅ What is it?

`just_audio` is a powerful, feature-rich audio player plugin.

---

### 🔧 Setup in `pubspec.yaml`

```yaml
dependencies:
  just_audio: ^0.9.34
```

Also run: `flutter pub get`

---

### ✅ Example 1: Play Network Audio

```dart
import 'package:flutter/material.dart';
import 'package:just_audio/just_audio.dart';

class NetworkAudioExample extends StatefulWidget {
  @override
  _NetworkAudioExampleState createState() => _NetworkAudioExampleState();
}

class _NetworkAudioExampleState extends State<NetworkAudioExample> {
  final player = AudioPlayer();

  @override
  void initState() {
    super.initState();
    player.setUrl('https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3');
    player.play();
  }

  @override
  void dispose() {
    player.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Network Audio')),
      body: Center(child: Text('Playing audio...')),
    );
  }
}
```

---

### ✅ Example 2: Play Local Asset Audio

* Add: `assets/audio/song.mp3`
* In `pubspec.yaml`:

```yaml
assets:
  - assets/audio/song.mp3
```

* Code:

```dart
await player.setAsset('assets/audio/song.mp3');
player.play();
```

---

### ✅ Example 3: Pause, Resume, Stop

```dart
player.pause();
player.play();
player.stop();
```

---

### ✅ Example 4: Volume and Looping

```dart
player.setVolume(0.5);      // Set half volume
player.setLoopMode(LoopMode.one); // Loop current song
```

---

## 📊 Summary Table

| Feature         | Package        | Example Code                         |
| --------------- | -------------- | ------------------------------------ |
| Video (network) | `video_player` | `VideoPlayerController.network()`    |
| Video (assets)  | `video_player` | `VideoPlayerController.asset()`      |
| Audio (network) | `just_audio`   | `player.setUrl()`                    |
| Audio (assets)  | `just_audio`   | `player.setAsset()`                  |
| Pause/Play      | Both           | `.pause()`, `.play()`                |
| Looping         | Both           | `.setLooping(true)` / `LoopMode.one` |

---

