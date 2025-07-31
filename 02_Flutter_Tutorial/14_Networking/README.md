# 🌐 Networking in Flutter

---

## 1. **HTTP Requests (http package)**

### ✅ What is the `http` package?

* The most commonly used package for making network requests in Flutter.
* Supports GET, POST, PUT, DELETE, etc.
* Easy to use for REST API calls.

---

### 🔧 How to use?

Add in `pubspec.yaml`:

```yaml
dependencies:
  http: ^0.13.5
```

Import in Dart:

```dart
import 'package:http/http.dart' as http;
```

---

### 🧪 Example 1: Simple GET Request

```dart
Future<void> fetchData() async {
  final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

  if (response.statusCode == 200) {
    print('Response data: ${response.body}');
  } else {
    print('Failed to load data');
  }
}
```

---

### 🧪 Example 2: Simple POST Request

```dart
Future<void> sendData() async {
  final response = await http.post(
    Uri.parse('https://jsonplaceholder.typicode.com/posts'),
    headers: {'Content-Type': 'application/json'},
    body: '{"title": "foo", "body": "bar", "userId": 1}',
  );

  if (response.statusCode == 201) {
    print('Data posted: ${response.body}');
  } else {
    print('Failed to post data');
  }
}
```

---

## 2. **Fetching & Displaying JSON Data**

### ✅ How to parse JSON data?

* Flutter uses Dart's built-in `dart:convert` package for JSON parsing.
* Convert JSON string into Dart objects using `jsonDecode`.
* You can create model classes for better structure.

---

### 🧪 Example 3: Fetch & Display JSON in ListView

**Step 1:** Create model class

```dart
class Post {
  final int id;
  final String title;

  Post({required this.id, required this.title});

  factory Post.fromJson(Map<String, dynamic> json) {
    return Post(
      id: json['id'],
      title: json['title'],
    );
  }
}
```

---

**Step 2:** Fetch data and parse JSON

```dart
Future<List<Post>> fetchPosts() async {
  final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));

  if (response.statusCode == 200) {
    final List<dynamic> jsonData = jsonDecode(response.body);
    return jsonData.map((json) => Post.fromJson(json)).toList();
  } else {
    throw Exception('Failed to load posts');
  }
}
```

---

**Step 3:** Display in ListView

```dart
class PostList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return FutureBuilder<List<Post>>(
      future: fetchPosts(),
      builder: (context, snapshot) {
        if (snapshot.hasData) {
          final posts = snapshot.data!;
          return ListView.builder(
            itemCount: posts.length,
            itemBuilder: (context, index) {
              return ListTile(
                title: Text(posts[index].title),
                subtitle: Text('Post ID: ${posts[index].id}'),
              );
            },
          );
        } else if (snapshot.hasError) {
          return Center(child: Text('Error: ${snapshot.error}'));
        }
        return Center(child: CircularProgressIndicator());
      },
    );
  }
}
```

---

## 3. **Error Handling**

### ✅ Why error handling is important?

* Network requests can fail due to connectivity, server errors, or invalid data.
* Proper error handling improves UX and app stability.

---

### 🔧 How to handle errors?

* Use `try-catch` blocks.
* Check HTTP status codes.
* Display meaningful messages to users.

---

### 🧪 Example 4: Error Handling with try-catch

```dart
Future<List<Post>> fetchPostsWithErrorHandling() async {
  try {
    final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));

    if (response.statusCode == 200) {
      final List<dynamic> jsonData = jsonDecode(response.body);
      return jsonData.map((json) => Post.fromJson(json)).toList();
    } else {
      throw Exception('Server error: ${response.statusCode}');
    }
  } catch (e) {
    throw Exception('Failed to load data: $e');
  }
}
```

---

## 4. **Dio Package**

### ✅ What is Dio?

* A powerful HTTP client for Dart with extra features:

  * Interceptors
  * Global configuration
  * Form data
  * Request cancellation
  * File downloading/uploading
  * Timeout control

---

### 🔧 How to use?

Add in `pubspec.yaml`:

```yaml
dependencies:
  dio: ^5.0.0
```

Import:

```dart
import 'package:dio/dio.dart';
```

---

### 🧪 Example 5: GET request using Dio

```dart
Future<void> fetchDataWithDio() async {
  final dio = Dio();

  try {
    final response = await dio.get('https://jsonplaceholder.typicode.com/posts/1');
    print('Dio response: ${response.data}');
  } catch (e) {
    print('Dio error: $e');
  }
}
```

---

### 🧪 Example 6: POST request using Dio

```dart
Future<void> sendDataWithDio() async {
  final dio = Dio();

  try {
    final response = await dio.post(
      'https://jsonplaceholder.typicode.com/posts',
      data: {'title': 'foo', 'body': 'bar', 'userId': 1},
    );
    print('Post success: ${response.data}');
  } catch (e) {
    print('Post failed: $e');
  }
}
```

---

## 5. **REST API Integration**

### ✅ How to integrate REST APIs?

* Use HTTP/Dio to make requests to endpoints.
* Map JSON to Dart models.
* Handle loading states and errors.
* Update UI with data asynchronously.

---

### 🧪 Example 7: Complete REST API integration pattern

* Define model class.
* Create a repository/service class for API calls.
* Use FutureBuilder or state management to handle UI updates.

---

**Service class example:**

```dart
class ApiService {
  final Dio _dio = Dio();

  Future<List<Post>> getPosts() async {
    final response = await _dio.get('https://jsonplaceholder.typicode.com/posts');
    return (response.data as List).map((json) => Post.fromJson(json)).toList();
  }
}
```

---

**Usage in Widget:**

```dart
class PostScreen extends StatelessWidget {
  final ApiService apiService = ApiService();

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<List<Post>>(
      future: apiService.getPosts(),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return CircularProgressIndicator();
        } else if (snapshot.hasError) {
          return Text('Error: ${snapshot.error}');
        } else {
          final posts = snapshot.data!;
          return ListView.builder(
            itemCount: posts.length,
            itemBuilder: (context, index) {
              return ListTile(title: Text(posts[index].title));
            },
          );
        }
      },
    );
  }
}
```

---

# Summary Table

| Concept              | Package/Class                   | Usage                            |
| -------------------- | ------------------------------- | -------------------------------- |
| HTTP Requests        | `http` package                  | GET, POST requests               |
| JSON Parsing         | `dart:convert`                  | Decode JSON to Dart objects      |
| Error Handling       | try-catch, status codes         | Manage exceptions and failures   |
| Advanced HTTP Client | `dio` package                   | Interceptors, cancel, timeout    |
| REST API Integration | Service classes + FutureBuilder | Clean architecture for API calls |

---


