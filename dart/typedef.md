# 📘 Typedef in Dart – Interview Guide

## ✅ What is a `typedef` in Dart?

`typedef` in Dart is used to define a custom **function type alias**. It helps you:

* Simplify function signatures
* Improve code readability
* Use callbacks or higher-order functions cleanly

---

## 📌 Syntax

```dart
typedef MyFunction = void Function(String name);
```

Above, `MyFunction` is an alias for a function that takes a `String` and returns `void`.

---

## 📦 Example – Basic Usage

```dart
typedef Greet = void Function(String name);

void sayHello(String name) {
  print('Hello, $name');
}

void greetUser(Greet greetFn) {
  greetFn('Alok');
}

void main() {
  greetUser(sayHello); // Output: Hello, Alok
}
```

---

## 🎯 Why Use Typedefs?

| Benefit         | Description                                               |
| --------------- | --------------------------------------------------------- |
| 📄 Readability  | Shorter and meaningful function type names                |
| 🔄 Reusability  | Use the same function type in multiple places             |
| 🔗 Callbacks    | Perfect for passing callback functions                    |
| 🧼 Cleaner Code | Especially useful with nested or long function signatures |

---

## 🔁 Typedef with Return Type

```dart
typedef IntOperation = int Function(int a, int b);

int add(int a, int b) => a + b;
int subtract(int a, int b) => a - b;

void calculate(IntOperation op) {
  print(op(10, 5));
}

void main() {
  calculate(add);      // Output: 15
  calculate(subtract); // Output: 5
}
```

---

## 🧱 Typedef for Future Functions

```dart
typedef AsyncTask = Future<String> Function(int id);

Future<String> fetchData(int id) async {
  await Future.delayed(Duration(seconds: 1));
  return 'Fetched ID: $id';
}

void executeTask(AsyncTask task) async {
  final result = await task(2);
  print(result);
}
```

---

## 💡 In Flutter BLoC/Callbacks Example

```dart
typedef EventCallback = void Function(String message);

class MyWidget extends StatelessWidget {
  final EventCallback onClick;

  const MyWidget({required this.onClick});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: () => onClick("Button clicked"),
      child: Text("Click Me"),
    );
  }
}
```

---

## 📚 Tips for Interview

* Typedef = custom function signature alias
* Common in callbacks, functional programming, and BLoC pattern
* Can be used with `Future`, `Stream`, or complex generic functions

---

## 🔐 Dart Typedef vs Function

| Feature           | Typedef | Direct Function |
| ----------------- | ------- | --------------- |
| Reusability       | ✅       | ❌               |
| Readability       | ✅       | ❌               |
| Used in Callbacks | ✅       | ✅               |

---

## 📌 Final Thought

Using `typedef` makes your Dart code modular, maintainable, and clean — a must-have skill for professional Flutter development.