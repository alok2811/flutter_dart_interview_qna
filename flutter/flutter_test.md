# 📘 Flutter Testing Guide & Interview Questions

This document covers everything you need to know about **Flutter testing**—from basics to advanced concepts—and includes commonly asked **interview questions**.

---

## ✅ Why Testing is Important in Flutter

* Ensures app works as expected
* Prevents future bugs after updates
* Automates regression checking
* Saves time on manual testing

---

## 🧪 Types of Tests in Flutter

### 1. **Unit Test**

* Tests a single function, method, or class.
* Fast and isolated from Flutter framework.

```dart
import 'package:test/test.dart';

void main() {
  test('adds two numbers', () {
    var sum = 2 + 3;
    expect(sum, 5);
  });
}
```

### 2. **Widget Test (Component Test)**

* Tests a single widget.
* Runs in a simulated environment (not real device).

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:myapp/main.dart';

void main() {
  testWidgets('Counter increments smoke test', (WidgetTester tester) async {
    await tester.pumpWidget(MyApp());

    expect(find.text('0'), findsOneWidget);
    await tester.tap(find.byIcon(Icons.add));
    await tester.pump();
    expect(find.text('1'), findsOneWidget);
  });
}
```

### 3. **Integration Test**

* Tests full app (UI + backend + navigation).
* Runs on real or simulated device.

```bash
flutter test integration_test
```

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:integration_test/integration_test.dart';
import 'package:myapp/main.dart';

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets('Full app test', (WidgetTester tester) async {
    await tester.pumpWidget(MyApp());
    // Interact with UI and verify behavior
  });
}
```

---

## 🚀 How to Run Tests

* **Unit/Widget tests:**

```bash
flutter test
```

* **Specific test file:**

```bash
flutter test test/my_test.dart
```

* **Integration tests:**

```bash
flutter test integration_test/app_test.dart
```

---

## 🔍 Useful Testing Commands

| Command                        | Purpose                           |
| ------------------------------ | --------------------------------- |
| `flutter test`                 | Run all unit/widget tests         |
| `flutter test test/file.dart`  | Run specific test file            |
| `flutter test --coverage`      | Show code coverage                |
| `flutter drive`                | Run integration tests with driver |
| `flutter pub run build_runner` | Used when mocking JSON or codegen |

---

## ❓ Common Interview Questions (Basic to Advanced)

### ✅ Basic

1. What are the types of tests in Flutter?
2. What’s the difference between unit, widget, and integration testing?
3. How do you write a widget test?
4. How do you run tests in Flutter?
5. What is `WidgetTester` used for?

### 🧠 Intermediate

6. What is golden testing in Flutter?
7. How do you mock a network call?
8. Explain `pump()` vs `pumpAndSettle()`.
9. What is the use of `IntegrationTestWidgetsFlutterBinding.ensureInitialized()`?
10. How do you test navigation between screens?

### 🚀 Advanced

11. How do you handle async code in tests?
12. Explain the use of mocks and stubs.
13. How can you integrate CI/CD for automated testing?
14. How do you test a Bloc or Provider?
15. How do you test platform channels or native code?

---

## 🧰 Tips for Testing in Flutter

* Keep tests independent and isolated.
* Use mock data to simulate API responses.
* Use `mockito` or `mocktail` for mocking.
* Always test critical logic and user flows.
* Don’t over-test UI animations unless required.

---

## 📦 Suggested Folder Structure

```
test/
├── unit/
├── widget/
├── integration/
```

---

Let me know if you want mock interview tests or practical exercises next!