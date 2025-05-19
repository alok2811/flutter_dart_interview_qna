# 🔧 Flutter Web Rendering Engines: HTML vs CanvasKit

Flutter provides two rendering backends for Flutter Web:

* **HTML Renderer**
* **CanvasKit Renderer**

---

## 🕁️ HTML Renderer

### ✅ Pros:

* **Smaller bundle size**.
* Works well with **text-heavy** or **simple UI** apps.
* Faster initial load time.
* Better integration with **native browser semantics** (like accessibility, SEO).

### ❌ Cons:

* Limited support for complex graphics and animations.
* May not match native Flutter performance.
* Some Flutter widgets might not render exactly as on mobile.

---

## 💎 CanvasKit Renderer

### ✅ Pros:

* **High-fidelity rendering** that closely matches Flutter mobile.
* Better for **graphics-heavy apps** and custom UI.
* More consistent cross-platform visuals.

### ❌ Cons:

* **Larger bundle size**.
* Slower initial load.
* Uses WebAssembly (WASM), which can be less SEO/accessibility friendly.

---

## 🧠 Comparison Table

| Feature           | HTML Renderer                   | CanvasKit Renderer             |
| ----------------- | ------------------------------- | ------------------------------ |
| Bundle Size       | Smaller                         | Larger (\~2-3MB extra)         |
| Load Time         | Faster                          | Slower                         |
| Rendering Quality | Moderate (good for text/UI)     | High-fidelity (matches mobile) |
| Graphics Support  | Limited                         | Full Skia support              |
| Accessibility/SEO | Better                          | Limited                        |
| Use Case          | Lightweight, content-based apps | Games, custom UI apps          |

---

## 🔧 How to Set Renderer

### 1. From Command Line

Use the `--web-renderer` flag:

```bash
flutter build web --web-renderer html
flutter build web --web-renderer canvaskit
```

### 2. In `index.html`

You can set a preferred renderer programmatically based on device.

---

## 🔎 Choosing the Right Renderer

* Choose **HTML** for:

    * Faster loads
    * Content-heavy or form-based apps
    * Better SEO/accessibility

* Choose **CanvasKit** for:

    * Apps with custom designs
    * Heavy use of animations or canvas
    * Pixel-perfect UI matching native Flutter

---

## 🔧 Tip

You can test both renderers with:

```bash
flutter run -d chrome --web-renderer html
flutter run -d chrome --web-renderer canvaskit
```

Use this to compare performance before final build.