### 🌐 Configure Web URL Strategies in Flutter (In Detail)

By default, Flutter web apps use **hash-based URLs** (`/#/route`) which are not clean or SEO-friendly. You can configure Flutter to use **clean paths** (like `/home`, `/about`) by **changing the URL strategy**.

---

## 🔍 Why Change URL Strategy?

| Strategy | Example URL                  | Pros                    | Cons                        |
| -------- | ---------------------------- | ----------------------- | --------------------------- |
| **Hash** | `https://example.com/#/home` | No server config needed | Not clean, not SEO-friendly |
| **Path** | `https://example.com/home`   | Clean, SEO-friendly     | Requires server setup       |

---

## 🧩 Flutter Packages and Strategies

Flutter supports different URL strategies via:

```dart
import 'package:flutter_web_plugins/url_strategy.dart';
```

You can choose between:

1. `PathUrlStrategy` → Clean URL (Recommended)
2. `HashUrlStrategy` → Hash-based routing (default)

---

## ✅ Steps to Use Clean URL (`PathUrlStrategy`)

### 1️⃣ Add Import and Set URL Strategy in `main.dart`

In your `main.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_web_plugins/url_strategy.dart';

void main() {
  // Set clean URLs (no #)
  setUrlStrategy(PathUrlStrategy());

  runApp(MyApp());
}
```

📝 This line changes how Flutter handles URLs internally.

---

### 2️⃣ Configure Your Web Server

Your web server must redirect **all requests to `index.html`** so Flutter can handle routing.

### For **Apache** (`.htaccess`):

```apache
<IfModule mod_rewrite.c>
  RewriteEngine on
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule ^.*$ /index.html [L]
</IfModule>
```

---

### For **Nginx**:

```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```

---

### For **Firebase Hosting** (`firebase.json`):

```json
"rewrites": [
  {
    "source": "**",
    "destination": "/index.html"
  }
]
```

---

### For **GitHub Pages** (Not directly supported)

GitHub Pages doesn't support server-side routing. You should **stick with hash URLs** or use a redirect workaround (e.g., using `404.html` to redirect).

---

## 🚧 If You Want to Use Hash-Based URLs (Default)

Just remove or comment out the `setUrlStrategy(PathUrlStrategy())` line:

```dart
// setUrlStrategy(PathUrlStrategy());  // use default (#)
```

Your URLs will look like:

```
https://example.com/#/home
```

---

## ✅ Summary

| Feature                   | Clean Path (`/home`) | Hash Path (`#/home`) |
| ------------------------- | -------------------- | -------------------- |
| Flutter config needed     | Yes                  | No                   |
| Web server setup required | Yes (for redirects)  | No                   |
| SEO Friendly              | ✅ Yes                | ❌ No                 |
| Works on GitHub Pages     | ❌ (needs workaround) | ✅ Yes                |

---

## 📦 Bonus: Use with `go_router`

If you’re using `go_router` (recommended Flutter navigation package), it works great with `PathUrlStrategy`:

```dart
import 'package:go_router/go_router.dart';
import 'package:flutter_web_plugins/url_strategy.dart';

void main() {
  setUrlStrategy(PathUrlStrategy());  // Enable clean URLs
  runApp(MyApp());
}
```

---

