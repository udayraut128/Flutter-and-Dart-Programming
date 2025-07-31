# 🔥 Firebase Integration with Flutter

---

## 1. **Firebase Core**

### ✅ What is Firebase Core?

* The foundational Flutter plugin to initialize Firebase services.
* It connects your Flutter app to your Firebase project.
* Must be initialized before using any Firebase service.

---

### 🔧 Setup Steps:

* Add Firebase to your Flutter app via Firebase Console.
* Add Firebase dependencies in `pubspec.yaml`:

```yaml
dependencies:
  firebase_core: ^2.10.0
```

* Initialize Firebase in your app:

```dart
import 'package:firebase_core/firebase_core.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```

---

### 🧪 Example 1: Basic Firebase Core Initialization

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
      future: Firebase.initializeApp(),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.done) {
          return MaterialApp(home: HomeScreen());
        }
        return CircularProgressIndicator();
      },
    );
  }
}
```

---

## 2. **Firebase Authentication**

### ✅ What is Firebase Auth?

* Provides backend services to authenticate users.
* Supports multiple sign-in methods: email/password, Google, Facebook, phone, etc.
* Simplifies user management.

---

### 🔧 Setup:

Add in `pubspec.yaml`:

```yaml
dependencies:
  firebase_auth: ^4.4.0
```

---

### 🧪 Example 2: Email/Password Authentication

```dart
import 'package:firebase_auth/firebase_auth.dart';

final FirebaseAuth _auth = FirebaseAuth.instance;

Future<User?> signInWithEmailPassword(String email, String password) async {
  try {
    UserCredential userCredential = await _auth.signInWithEmailAndPassword(
      email: email,
      password: password,
    );
    return userCredential.user;
  } on FirebaseAuthException catch (e) {
    print('Failed to sign in: ${e.message}');
    return null;
  }
}
```

---

### 🧪 Example 3: Registering a New User

```dart
Future<User?> registerUser(String email, String password) async {
  try {
    UserCredential userCredential = await _auth.createUserWithEmailAndPassword(
      email: email,
      password: password,
    );
    return userCredential.user;
  } on FirebaseAuthException catch (e) {
    print('Failed to register: ${e.message}');
    return null;
  }
}
```

---

### 🧪 Example 4: Sign Out

```dart
Future<void> signOutUser() async {
  await _auth.signOut();
}
```

---

## 3. **Cloud Firestore**

### ✅ What is Firestore?

* A NoSQL cloud database to store, sync, and query data in real-time.
* Stores data in collections and documents.
* Integrates well with Flutter for realtime updates.

---

### 🔧 Setup:

Add in `pubspec.yaml`:

```yaml
dependencies:
  cloud_firestore: ^4.5.0
```

Import:

```dart
import 'package:cloud_firestore/cloud_firestore.dart';
```

---

### 🧪 Example 5: Adding Data to Firestore

```dart
final FirebaseFirestore _firestore = FirebaseFirestore.instance;

Future<void> addUser() async {
  await _firestore.collection('users').add({
    'name': 'John Doe',
    'email': 'john@example.com',
    'age': 25,
  });
}
```

---

### 🧪 Example 6: Reading Data from Firestore (Once)

```dart
Future<void> getUsers() async {
  QuerySnapshot snapshot = await _firestore.collection('users').get();
  for (var doc in snapshot.docs) {
    print(doc.data());
  }
}
```

---

### 🧪 Example 7: Real-time Data Stream

```dart
StreamBuilder<QuerySnapshot>(
  stream: _firestore.collection('users').snapshots(),
  builder: (context, snapshot) {
    if (!snapshot.hasData) return CircularProgressIndicator();

    final docs = snapshot.data!.docs;

    return ListView.builder(
      itemCount: docs.length,
      itemBuilder: (context, index) {
        var data = docs[index].data() as Map<String, dynamic>;
        return ListTile(
          title: Text(data['name']),
          subtitle: Text(data['email']),
        );
      },
    );
  },
);
```

---

### 🧪 Example 8: Updating a Document

```dart
Future<void> updateUser(String docId) async {
  await _firestore.collection('users').doc(docId).update({'age': 26});
}
```

---

# Summary Table

| Firebase Service | Purpose              | Key Classes/Methods                                            |
| ---------------- | -------------------- | -------------------------------------------------------------- |
| Firebase Core    | Initialize Firebase  | `Firebase.initializeApp()`                                     |
| Firebase Auth    | User authentication  | `FirebaseAuth`, `signInWithEmailAndPassword`                   |
| Cloud Firestore  | Cloud NoSQL database | `FirebaseFirestore`, `.collection()`, `.add()`, `.snapshots()` |

---

## 🔹 1. **Firebase Realtime Database**

### ✅ What is it?

* A cloud-hosted NoSQL database that stores data in **JSON format**.
* Syncs data **in real-time** across all clients.

### 🔧 Setup:

```yaml
dependencies:
  firebase_database: ^11.0.0
```

Import:

```dart
import 'package:firebase_database/firebase_database.dart';
```

### 📘 Examples:

#### 🧪 Example 1: Write Data

```dart
final db = FirebaseDatabase.instance.ref();

Future<void> writeUserData() async {
  await db.child('users/user1').set({
    'name': 'Alice',
    'email': 'alice@example.com',
  });
}
```

---

#### 🧪 Example 2: Read Data Once

```dart
void readUserData() async {
  DatabaseEvent event = await db.child('users/user1').once();
  print(event.snapshot.value);
}
```

---

#### 🧪 Example 3: Listen to Real-time Changes

```dart
db.child('users/user1').onValue.listen((DatabaseEvent event) {
  final data = event.snapshot.value;
  print("Real-time data: $data");
});
```

---

#### 🧪 Example 4: Update Data

```dart
await db.child('users/user1').update({'name': 'Bob'});
```

---

## 🔹 2. **Firebase Storage**

### ✅ What is it?

* Stores and serves **user-generated files** such as images, videos, PDFs.

### 🔧 Setup:

```yaml
dependencies:
  firebase_storage: ^11.1.0
```

Import:

```dart
import 'package:firebase_storage/firebase_storage.dart';
```

### 📘 Examples:

#### 🧪 Example 1: Upload File

```dart
Future<void> uploadFile(File file) async {
  final ref = FirebaseStorage.instance.ref().child('uploads/image.jpg');
  await ref.putFile(file);
}
```

---

#### 🧪 Example 2: Download URL

```dart
Future<String> getDownloadURL() async {
  final ref = FirebaseStorage.instance.ref().child('uploads/image.jpg');
  return await ref.getDownloadURL();
}
```

---

#### 🧪 Example 3: Delete File

```dart
Future<void> deleteFile() async {
  final ref = FirebaseStorage.instance.ref().child('uploads/image.jpg');
  await ref.delete();
}
```

---

#### 🧪 Example 4: Upload with Metadata

```dart
await ref.putFile(
  file,
  SettableMetadata(contentType: 'image/jpeg'),
);
```

---

## 🔹 3. **Firebase Messaging (Push Notifications)**

### ✅ What is it?

* Send and receive **push notifications**.
* Uses **Firebase Cloud Messaging (FCM)**.

### 🔧 Setup:

```yaml
dependencies:
  firebase_messaging: ^14.7.0
```

Import:

```dart
import 'package:firebase_messaging/firebase_messaging.dart';
```

### 📘 Examples:

#### 🧪 Example 1: Request Permission

```dart
await FirebaseMessaging.instance.requestPermission();
```

---

#### 🧪 Example 2: Get FCM Token

```dart
String? token = await FirebaseMessaging.instance.getToken();
print("FCM Token: $token");
```

---

#### 🧪 Example 3: Listen to Foreground Messages

```dart
FirebaseMessaging.onMessage.listen((RemoteMessage message) {
  print("Message: ${message.notification?.title}");
});
```

---

#### 🧪 Example 4: Handle Background Messages

```dart
Future<void> _firebaseMessagingBackgroundHandler(RemoteMessage message) async {
  print("Background Message: ${message.messageId}");
}
```

Register in `main()`:

```dart
FirebaseMessaging.onBackgroundMessage(_firebaseMessagingBackgroundHandler);
```

---

## 🔹 4. **Firebase Analytics**

### ✅ What is it?

* Tracks **user events and behavior** (like page views, button clicks, etc.).

### 🔧 Setup:

```yaml
dependencies:
  firebase_analytics: ^10.6.0
```

Import:

```dart
import 'package:firebase_analytics/firebase_analytics.dart';
```

### 📘 Examples:

#### 🧪 Example 1: Log Custom Event

```dart
FirebaseAnalytics analytics = FirebaseAnalytics.instance;

await analytics.logEvent(
  name: 'login',
  parameters: {'method': 'email'},
);
```

---

#### 🧪 Example 2: Track Page View

```dart
await analytics.setCurrentScreen(screenName: 'HomeScreen');
```

---

#### 🧪 Example 3: Set User Property

```dart
await analytics.setUserProperty(name: 'user_type', value: 'admin');
```

---

#### 🧪 Example 4: Track Purchase Event

```dart
await analytics.logPurchase(
  currency: 'USD',
  value: 49.99,
  transactionId: 'TX12345',
);
```

---

## 🔹 5. **Firebase Crashlytics**

### ✅ What is it?

* Automatically logs **runtime errors, crashes, exceptions**.
* Helps you monitor and fix issues in production apps.

### 🔧 Setup:

```yaml
dependencies:
  firebase_crashlytics: ^4.3.0
```

Import:

```dart
import 'package:firebase_crashlytics/firebase_crashlytics.dart';
```

Enable in `main()`:

```dart
void main() async {
  FlutterError.onError = FirebaseCrashlytics.instance.recordFlutterError;
  runApp(MyApp());
}
```

---

### 📘 Examples:

#### 🧪 Example 1: Record a Custom Error

```dart
try {
  throw Exception("Something went wrong!");
} catch (e, stack) {
  FirebaseCrashlytics.instance.recordError(e, stack);
}
```

---

#### 🧪 Example 2: Log Custom Messages

```dart
FirebaseCrashlytics.instance.log("User clicked on BUY button");
```

---

#### 🧪 Example 3: Force a Test Crash

```dart
FirebaseCrashlytics.instance.crash();
```

---

#### 🧪 Example 4: Set User Identifier

```dart
FirebaseCrashlytics.instance.setUserIdentifier('user_1234');
```

---

## ✅ Summary Table

| Service              | Purpose                    | Key Features                                      |
| -------------------- | -------------------------- | ------------------------------------------------- |
| Realtime Database    | Real-time JSON database    | `.set()`, `.onValue`, `.once()`                   |
| Firebase Storage     | Upload & download files    | `.putFile()`, `.getDownloadURL()`, `.delete()`    |
| Firebase Messaging   | Push notifications         | `onMessage`, `getToken`, background handler       |
| Firebase Analytics   | Track user activity        | `logEvent`, `setCurrentScreen`, `setUserProperty` |
| Firebase Crashlytics | Catch crashes & log errors | `recordError`, `log`, `crash()`                   |

---


