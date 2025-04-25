---
layout: post
title: "📡 Android Activity Lifecycle Guide"
author: anil
categories: [Kotlin, Android, Architecture]
tags: [Mobile Development, Android]
image: data:image/jpeg;base64,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
---
# 🧠 Mastering the Android Activity Lifecycle: A Modern Developer’s Guide

The Android Activity Lifecycle is fundamental to building responsive, memory-efficient, and user-friendly apps. Understanding how an `Activity` moves through its lifecycle is essential for everything from saving user data to avoiding memory leaks.

In this blog, we’ll break down the lifecycle stages with Kotlin examples and sprinkle in tips and tricks for making your apps shine in the real world.

---

## 🧩 What Is the Android Activity Lifecycle?

Every `Activity` in Android goes through a set of predefined states — from **creation** to **destruction**. Android calls lifecycle callback methods as the activity enters and exits these states, letting you handle UI setup, resource management, and state persistence appropriately.

---

## 🔄 Lifecycle Flow (Visual)

```
onCreate()
   ↓
onStart()
   ↓
onResume()
   ↓
-- (Activity is Running) --
   ↑
onPause()
   ↑
onStop()
   ↑
onDestroy()
```

---

## 🚀 Lifecycle Methods Explained (with Kotlin Code)

### 1️⃣ `onCreate()`

> Called when the activity is first created. Set up views, bindings, ViewModel, and data sources here.

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
    Log.d("Lifecycle", "onCreate")
}
```

💡 **Tips**:
- Keep it lightweight. Avoid long-running operations.
- Initialize only essential components.
- Use ViewBinding/DataBinding for better maintainability.

---

### 2️⃣ `onStart()`

> The activity is becoming visible.

```kotlin
override fun onStart() {
    super.onStart()
    Log.d("Lifecycle", "onStart")
}
```

💡 **Tip**: Ideal for UI updates that don’t need user interaction.

---

### 3️⃣ `onResume()`

> The activity is now in the foreground and interactive.

```kotlin
override fun onResume() {
    super.onResume()
    Log.d("Lifecycle", "onResume")
}
```

💡 **Use Cases**:
- Start animations
- Resume camera or sensors
- Check for app updates or messages

---

### 4️⃣ `onPause()`

> Another activity is coming into the foreground. You should pause heavy resources here.

```kotlin
override fun onPause() {
    super.onPause()
    Log.d("Lifecycle", "onPause")
}
```

💡 **Tips**:
- Pause video/audio playback.
- Save UI state or data.
- Don’t do heavy operations — it should be fast.

---

### 5️⃣ `onStop()`

> The activity is no longer visible to the user.

```kotlin
override fun onStop() {
    super.onStop()
    Log.d("Lifecycle", "onStop")
}
```

💡 **Tip**: Release memory-heavy resources like background threads, sensors, or database connections.

---

### 6️⃣ `onRestart()`

> Called when the activity moves from stopped to started again.

```kotlin
override fun onRestart() {
    super.onRestart()
    Log.d("Lifecycle", "onRestart")
}
```

💡 **Use Case**: Refresh data or UI if needed.

---

### 7️⃣ `onDestroy()`

> The activity is finishing or being destroyed by the system.

```kotlin
override fun onDestroy() {
    super.onDestroy()
    Log.d("Lifecycle", "onDestroy")
}
```

💡 **Tips**:
- Clean up any memory leaks.
- Unregister listeners or observers.
- If using coroutines, cancel active scopes.

---

## ✅ Full Activity Lifecycle Example (Kotlin)

```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        Log.d("Lifecycle", "onCreate")
    }

    override fun onStart() {
        super.onStart()
        Log.d("Lifecycle", "onStart")
    }

    override fun onResume() {
        super.onResume()
        Log.d("Lifecycle", "onResume")
    }

    override fun onPause() {
        super.onPause()
        Log.d("Lifecycle", "onPause")
    }

    override fun onStop() {
        super.onStop()
        Log.d("Lifecycle", "onStop")
    }

    override fun onRestart() {
        super.onRestart()
        Log.d("Lifecycle", "onRestart")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d("Lifecycle", "onDestroy")
    }
}
```

---

## 💡 Pro Tips for Modern Android Development

### ✅ 1. Use ViewModel to Handle Configuration Changes

```kotlin
private val viewModel: MainViewModel by viewModels()
```

### ✅ 2. Leverage Lifecycle-Aware Components

```kotlin
class MyObserver : DefaultLifecycleObserver {
    override fun onStart(owner: LifecycleOwner) {
        Log.d("Observer", "Started")
    }
}
```

Attach it in your activity:

```kotlin
lifecycle.addObserver(MyObserver())
```

### ✅ 3. Avoid Memory Leaks
- Never hold a reference to a `Context` or `Activity` in a static variable.
- Always unregister callbacks and listeners in `onPause()` or `onDestroy()`.

### ✅ 4. Use LifecycleScope for Coroutines

```kotlin
lifecycleScope.launch {
    // safe to run during lifecycle
}
```

---

## 🔚 Conclusion

Mastering the Activity lifecycle gives you fine-grained control over your app’s behavior, performance, and resource usage. Whether you're handling UI updates, loading data, or managing memory, the lifecycle methods provide the right hooks at the right time.


