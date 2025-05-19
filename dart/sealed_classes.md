# 🧱 Sealed Classes in Dart (For Flutter BLoC)

## 📌 What are Sealed Classes?

Sealed classes in Dart are classes where the subtypes are known and restricted to a fixed set. It allows exhaustive checking using `switch` statements, which is useful for maintaining predictable state/event structures in Flutter BLoC.

Introduced in **Dart 3**, sealed classes help you:

* Improve type safety
* Enforce exhaustive handling of states/events
* Write cleaner BLoC code

---

## ✅ How to Declare a Sealed Class

```dart
sealed class Animal {}

class Dog extends Animal {}
class Cat extends Animal {}
```

You can also use `base`, `interface`, or `final` classes to control inheritance.

---

## 📦 Sealed Class in Flutter BLoC – Example

Let’s use sealed classes for BLoC `Events` and `States`.

### 🔶 Sealed Event Class

```dart
sealed class CounterEvent {}

class IncrementEvent extends CounterEvent {}
class DecrementEvent extends CounterEvent {}
```

### 🔷 Sealed State Class

```dart
sealed class CounterState {}

class CounterInitial extends CounterState {
  final int value;
  CounterInitial(this.value);
}

class CounterUpdated extends CounterState {
  final int value;
  CounterUpdated(this.value);
}
```

### ✅ BLoC Using Sealed Classes

```dart
class CounterBloc extends Bloc<CounterEvent, CounterState> {
  CounterBloc() : super(CounterInitial(0)) {
    on<IncrementEvent>((event, emit) {
      if (state is CounterInitial) {
        emit(CounterUpdated((state as CounterInitial).value + 1));
      } else if (state is CounterUpdated) {
        emit(CounterUpdated((state as CounterUpdated).value + 1));
      }
    });

    on<DecrementEvent>((event, emit) {
      final currentValue = state is CounterUpdated
          ? (state as CounterUpdated).value
          : (state as CounterInitial).value;
      emit(CounterUpdated(currentValue - 1));
    });
  }
}
```

---

## 🧠 Why Use Sealed Classes in BLoC?

| Benefit                | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| 🔐 Type Safety         | Forces developers to handle all cases in `switch` statements |
| 🚫 Restrict Extension  | Only defined subclasses allowed                              |
| 🧼 Cleaner Code        | Easy-to-read state and event structure                       |
| ⚠️ Compile-Time Errors | If a case isn’t handled, Dart will warn you                  |

---

## 🧪 Using `switch` with Sealed Classes

```dart
switch (state) {
  case CounterInitial():
    return Text('Initial: ${state.value}');
  case CounterUpdated():
    return Text('Updated: ${state.value}');
}
```

Dart ensures all possible cases are handled.

---

## 🚀 Tips

* Use sealed classes for both **Events** and **States**
* Use pattern matching with `switch` (Dart 3.1+)
* Combine with `BlocSelector` for optimal rebuilds

---

## 📌 Requirements

* Dart SDK 3.0+
* Enable Dart 3 features in `pubspec.yaml`:

```yaml
environment:
  sdk: ">=3.0.0 <4.0.0"
```

---

## 📚 References

* [Official Dart Docs – Sealed Classes](https://dart.dev/language/class-modifiers#sealed)
* [Flutter BLoC Package](https://pub.dev/packages/flutter_bloc)

> Sealed classes enhance safety, maintainability, and structure in Flutter BLoC. Highly recommended for production apps.