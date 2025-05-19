# 🧠 Flutter BLoC (Business Logic Component) – Complete Guide

## 📌 What is BLoC?

**BLoC** is a state management pattern that separates business logic from UI, using `Streams` and `Events`. The `flutter_bloc` package simplifies BLoC with high-level widgets and patterns.

---

## 🧱 File Structure & Roles

```
lib/
├── blocs/
│   └── counter/
│       ├── counter_bloc.dart
│       ├── counter_event.dart
│       └── counter_state.dart
├── screens/
│   └── counter_screen.dart
├── main.dart
```

### 1. `counter_event.dart`

Defines all possible **events**.

```dart
abstract class CounterEvent {}

class Increment extends CounterEvent {}
class Decrement extends CounterEvent {}
```

### 2. `counter_state.dart`

Defines the current **state** of the BLoC.

```dart
class CounterState {
  final int counterValue;
  CounterState(this.counterValue);
}
```

### 3. `counter_bloc.dart`

Handles business logic. Converts `Events` to `States`.

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

class CounterBloc extends Bloc<CounterEvent, CounterState> {
  CounterBloc() : super(CounterState(0)) {
    on<Increment>((event, emit) => emit(CounterState(state.counterValue + 1)));
    on<Decrement>((event, emit) => emit(CounterState(state.counterValue - 1)));
  }
}
```

---

## 🧩 BlocProvider (Dependency Injection)

Use `BlocProvider` to **inject your bloc** into the widget tree.

### ✅ Single BLoC:

```dart
BlocProvider(
  create: (_) => CounterBloc(),
  child: CounterScreen(),
)
```

### ✅ Multiple BLoCs:

```dart
MultiBlocProvider(
  providers: [
    BlocProvider(create: (_) => CounterBloc()),
    BlocProvider(create: (_) => AnotherBloc()),
  ],
  child: MyApp(),
)
```

---

## 🖥️ Using BLoC in UI

### 1. `BlocBuilder`

Listens to state changes and rebuilds UI.

```dart
BlocBuilder<CounterBloc, CounterState>(
  builder: (context, state) {
    return Text('Value: ${state.counterValue}');
  },
)
```

### 2. `BlocListener`

Listens to state changes without rebuilding UI.

```dart
BlocListener<CounterBloc, CounterState>(
  listener: (context, state) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text('Updated: ${state.counterValue}')),
    );
  },
  child: YourWidget(),
)
```

### 3. `BlocConsumer`

Combines `BlocBuilder` + `BlocListener`.

```dart
BlocConsumer<CounterBloc, CounterState>(
  listener: (context, state) {
    // Show message
  },
  builder: (context, state) {
    return Text('${state.counterValue}');
  },
)
```

---

## 🎯 BlocSelector (Optimize Rebuilds)

Use it to listen to **specific part** of the state only.

```dart
BlocSelector<CounterBloc, CounterState, int>(
  selector: (state) => state.counterValue,
  builder: (context, counterValue) {
    return Text('Selected Value: $counterValue');
  },
)
```

---

## 📦 Best Practices

* Keep each BLoC in its own folder.
* Use `Equatable` to compare states.
* Use `sealed classes` for states/events (if Dart SDK supports).
* Avoid business logic in UI widgets.
* Use `BlocObserver` to log BLoC changes.

---

## 🧪 BlocObserver (Debugging)

Track transitions globally.

```dart
class SimpleBlocObserver extends BlocObserver {
  @override
  void onTransition(Bloc bloc, Transition transition) {
    super.onTransition(bloc, transition);
    print(transition);
  }
}

void main() {
  Bloc.observer = SimpleBlocObserver();
  runApp(MyApp());
}
```

---

## 🧠 Interview Points to Remember

* Difference between `BlocBuilder`, `BlocListener`, `BlocConsumer`
* Use cases for `BlocSelector`
* Advantages of BLoC pattern
* Handling loading, success, error states
* How to test BLoC
* Role of `Equatable`
* `BlocProvider vs MultiBlocProvider`
* Global `BlocObserver`
* Dependency Injection with `BlocProvider`

---

## 🚀 Resources

* Official docs: [https://bloclibrary.dev](https://bloclibrary.dev)
* VS Code Extension: Flutter BLoC Snippets

> This file serves as a complete reference to prepare for Flutter BLoC-related interviews. ✅