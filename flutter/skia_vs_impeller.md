# 📱 Flutter Rendering Engines: Skia vs Impeller

## 🔹 What is Skia?

**Skia** is a mature, open-source 2D graphics engine used by Flutter (and also by Chrome, Android, and Firefox). It's been the default rendering engine in Flutter since its inception.

### ✅ Features of Skia

* Renders UI using the **CPU & GPU**.
* Supports a wide range of platforms.
* Has robust and stable rendering.
* Relies on **shader compilation at runtime**, which may lead to **jank** (frame drops) during the first-time rendering of complex effects.

### ⚠️ Limitations

* **Shader compilation jank**: Especially noticeable on mobile devices when using complex gradients, shadows, or vector graphics.
* **Runtime shader compilation** is non-deterministic across platforms and devices.

---

## 🛣️ What is Impeller?

**Impeller** is Flutter’s next-generation rendering engine designed to **eliminate shader compilation jank** and provide smoother performance, especially on iOS and Android.

### ✅ Features of Impeller

* **Pre-compiles shaders**: Reduces runtime jank significantly.
* Uses **modern rendering APIs** like Metal (iOS) and Vulkan (Android).
* Optimized for **predictable performance and smooth animations**.
* Helps Flutter deliver **consistent 60fps or 120fps** experiences.

### 🔄 Status

* **Enabled by default on iOS** since Flutter 3.10.
* Still **experimental on Android** but rapidly progressing.

---

## 🤚 Skia vs Impeller Comparison

| Feature               | Skia                   | Impeller                          |
| --------------------- | ---------------------- | --------------------------------- |
| Shader Compilation    | Runtime                | Ahead-of-time (AOT)               |
| Performance           | May jank (esp. on iOS) | Smooth & jank-free                |
| API Support           | OpenGL/Metal/Vulkan    | Metal (iOS), Vulkan (Android)     |
| Default in Flutter    | Yes (all platforms)    | iOS (default), Android (optional) |
| Custom Shader Support | Yes (runtime)          | Limited (planned improvements)    |
| Target                | Stability              | Predictable Performance           |

---

## 🔧 How to Enable Impeller

### Android

```bash
flutter build apk --enable-impeller
```

### iOS

```bash
flutter build ios --enable-impeller
```

### To make it default in `pubspec.yaml`:

```yaml
flutter:
  enable-impeller: true
```

---

## 🧠 Conclusion

* Use **Skia** if you prioritize stability and compatibility with all existing features.
* Use **Impeller** if you need **smoother animations**, **less jank**, and are targeting **modern hardware**.
* As Flutter evolves, **Impeller is expected to fully replace Skia** as the default engine.