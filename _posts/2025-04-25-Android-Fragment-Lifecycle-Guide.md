---
layout: post
title: "📡 Android Fragment Lifecycle Guide"
author: anil
categories: [Kotlin, Android, Architecture]
tags: [Mobile Development, Android]
image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQUAK8S-IAjqEdMLQcn7oJNae6wNbebyd9Rpw&s
---
# 🔍 Mastering the Android Fragment Lifecycle: Modern Tips & Kotlin Code Examples

Fragments are essential for building modular and reusable UI components in Android. But with this power comes complexity — especially when managing the **Fragment Lifecycle**, which has some key differences from the Activity lifecycle.

In this guide, we'll explore each stage of the Fragment lifecycle, provide Kotlin code examples, and share modern development tips so you can avoid common pitfalls and write cleaner, more robust code.

---

## 🧩 Fragment Lifecycle Overview

A `Fragment` has two primary lifecycles:

- **Fragment lifecycle**: Deals with the fragment instance itself.
- **View lifecycle**: Deals with the UI (`View`) of the fragment.

These lifecycles don't always move together — and that's why developers often hit bugs with view bindings and lifecycle observers.

---

## 🔄 Fragment Lifecycle Flow (Visual)

```
onAttach()
   ↓
onCreate()
   ↓
onCreateView()
   ↓
onViewCreated()
   ↓
onStart()
   ↓
onResume()
   ↓
-- Fragment Running --
   ↑
onPause()
   ↑
onStop()
   ↑
onDestroyView()
   ↑
onDestroy()
   ↑
onDetach()
```

---

## 🧠 Lifecycle Callbacks (with Kotlin Examples)

### 1️⃣ `onAttach(context: Context)`

```kotlin
override fun onAttach(context: Context) {
    super.onAttach(context)
    Log.d("Lifecycle", "onAttach")
}
```

✅ Use this for getting context references, initializing callbacks or listeners tied to the host activity.

---

### 2️⃣ `onCreate(savedInstanceState: Bundle?)`

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    Log.d("Lifecycle", "onCreate")
}
```

✅ Use this for initializing ViewModels, arguments, or non-UI data.

---

### 3️⃣ `onCreateView(...)`

```kotlin
override fun onCreateView(
    inflater: LayoutInflater,
    container: ViewGroup?,
    savedInstanceState: Bundle?
): View {
    return inflater.inflate(R.layout.fragment_sample, container, false)
}
```

✅ Avoid accessing views here. Just inflate and return the view.

---

### 4️⃣ `onViewCreated(view: View, savedInstanceState: Bundle?)`

```kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
    super.onViewCreated(view, savedInstanceState)
    Log.d("Lifecycle", "onViewCreated")
}
```

✅ Use this for binding views, setting up adapters, and observing LiveData.

---

### 5️⃣ `onStart()` and `onResume()`

```kotlin
override fun onStart() {
    super.onStart()
    Log.d("Lifecycle", "onStart")
}

override fun onResume() {
    super.onResume()
    Log.d("Lifecycle", "onResume")
}
```

✅ Use for analytics, media, sensors, or UI updates.

---

### 6️⃣ `onPause()` and `onStop()`

```kotlin
override fun onPause() {
    super.onPause()
    Log.d("Lifecycle", "onPause")
}

override fun onStop() {
    super.onStop()
    Log.d("Lifecycle", "onStop")
}
```

✅ Use for pausing media and saving state.

---

### 7️⃣ `onDestroyView()`

```kotlin
override fun onDestroyView() {
    super.onDestroyView()
    Log.d("Lifecycle", "onDestroyView")
}
```

✅ Nullify view binding and release UI resources here.

---

### 8️⃣ `onDestroy()` and `onDetach()`

```kotlin
override fun onDestroy() {
    super.onDestroy()
    Log.d("Lifecycle", "onDestroy")
}

override fun onDetach() {
    super.onDetach()
    Log.d("Lifecycle", "onDetach")
}
```

✅ Clean up tasks and references to avoid memory leaks.

---

## 📦 Full Fragment Lifecycle Example (Kotlin)

```kotlin
class SampleFragment : Fragment(R.layout.fragment_sample) {

    override fun onAttach(context: Context) {
        super.onAttach(context)
        Log.d("Lifecycle", "onAttach")
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.d("Lifecycle", "onCreate")
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        Log.d("Lifecycle", "onViewCreated")
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

    override fun onDestroyView() {
        super.onDestroyView()
        Log.d("Lifecycle", "onDestroyView")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d("Lifecycle", "onDestroy")
    }

    override fun onDetach() {
        super.onDetach()
        Log.d("Lifecycle", "onDetach")
    }
}
```

---

## 🧙‍♂️ Tips & Tricks for Modern Fragment Development

### ✅ 1. Safe ViewBinding

```kotlin
private var _binding: FragmentSampleBinding? = null
private val binding get() = _binding!!

override fun onCreateView(...) = FragmentSampleBinding.inflate(inflater, container, false).also {
    _binding = it
}.root

override fun onDestroyView() {
    super.onDestroyView()
    _binding = null
}
```

---

### ✅ 2. Share Data with ViewModel

```kotlin
private val sharedViewModel: SharedViewModel by activityViewModels()
```

---

### ✅ 3. Use Lifecycle-Aware Observers

```kotlin
viewLifecycleOwner.lifecycleScope.launch {
    repeatOnLifecycle(Lifecycle.State.STARTED) {
        viewModel.stateFlow.collect {
            // UI updates
        }
    }
}
```

---

### ✅ 4. Don’t Store Fragments in Static Fields

Instead, use:

```kotlin
supportFragmentManager.beginTransaction()
    .replace(R.id.container, MyFragment())
    .commit()
```

---

## 🧠 Conclusion

Master the Fragment lifecycle to create high-performance, maintainable, and bug-free apps. Separate UI and business logic, use ViewModel, and always clean up bindings to avoid leaks.

