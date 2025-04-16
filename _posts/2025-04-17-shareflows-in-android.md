---
layout: post
title: "📡 Everything You Need to Know About SharedFlow in Android"
author: anil
categories: [Kotlin, Android, Architecture]
tags: [LiveData, MVVM, StateFlow, Jetpack, Lifecycle]
image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSriEnB4djA09Hwmz7xrfegmj78sTkevz3Ml3wfh-2ZJuEIJObds-mlUcu0P4fULmfOuS4&usqp=CAU
featured: false
---
# 📢 Everything You Need to Know About SharedFlow in Android

As modern Android development evolves, reactive and coroutine-based architectures are taking center stage. While `LiveData` and `StateFlow` are great for observing state, **`SharedFlow` is the go-to solution for one-time events**, like showing a toast, navigation, or triggering dialogs.

In this post, we’ll explore:

- What is SharedFlow?
- SharedFlow vs StateFlow vs LiveData
- Use cases for SharedFlow
- How SharedFlow works
- Code examples
- Best practices
- Common pitfalls

---

## 💡 What is SharedFlow?

`SharedFlow` is a **hot flow** introduced in **Kotlin Coroutines 1.4.0+** as part of the `kotlinx.coroutines.flow` package. Unlike `StateFlow`, which holds and replays the latest value, `SharedFlow` can emit **multiple values** and can be configured to **replay** a specific number of past values to new collectors.

> Think of `SharedFlow` as a **coroutine-based event broadcaster**—suitable for one-time events like navigation, snackbars, or messages.

---

## 🔄 SharedFlow vs StateFlow vs LiveData

| Feature               | SharedFlow                     | StateFlow                     | LiveData                     |
|-----------------------|--------------------------------|-------------------------------|------------------------------|
| Lifecycle aware       | ❌ No                          | ❌ No                          | ✅ Yes                        |
| Holds latest value    | ❌ Optional                    | ✅ Always                      | ✅ Yes                        |
| Supports multiple collectors | ✅ Yes                | ✅ Yes                         | ⚠️ Limited                   |
| Replay values         | ✅ Customizable                | ✅ Only latest                 | ⚠️ No                        |
| Event support         | ✅ Ideal for events            | ❌ Avoid for one-time events   | ⚠️ Workarounds needed        |
| Coroutine-native      | ✅ Yes                         | ✅ Yes                         | ⚠️ Optional                  |

---

## 🚀 Why Use SharedFlow?

- 🔥 **Hot stream** — always emits even if no one is collecting.
- 🧵 **Coroutine-native** — works well with `viewModelScope` and `lifecycleScope`.
- 📤 **Supports multiple collectors** — great for broadcasting.
- ⏪ **Replay support** — can replay past values to new collectors.
- 🎯 **Best suited for one-off events** — like toasts, navigation, and UI signals.

---

## 🧬 Anatomy of SharedFlow

SharedFlow is **read-only** by default, but you use `MutableSharedFlow` to emit values.

### ViewModel setup:

```kotlin
class MyViewModel : ViewModel() {
    private val _events = MutableSharedFlow<String>()
    val events = _events.asSharedFlow()

    fun sendEvent(message: String) {
        viewModelScope.launch {
            _events.emit(message)
        }
    }
}
Collect in Activity or Fragment:
kotlin
Copy
Edit
lifecycleScope.launchWhenStarted {
    viewModel.events.collect { event ->
        Toast.makeText(context, event, Toast.LENGTH_SHORT).show()
    }
}
⚙️ SharedFlow Configuration
MutableSharedFlow can be customized using:

kotlin
Copy
Edit
MutableSharedFlow<T>(
    replay = 0,               // Number of values to replay to new collectors
    extraBufferCapacity = 0,  // Buffer before suspending emitters
    onBufferOverflow = BufferOverflow.SUSPEND // Strategy: DROP_LATEST, DROP_OLDEST
)
Example with replay:

kotlin
Copy
Edit
val messages = MutableSharedFlow<String>(replay = 1)
📦 Use Cases for SharedFlow
🚦 Navigation events (e.g. navigate to next screen)

🔔 One-time messages like snackbars/toasts

✅ Form submission success

❌ Error reporting

🕹️ UI triggers (dialogs, modals)

🔧 Real-world Example: Navigation
kotlin
Copy
Edit
sealed class UiEvent {
    data object NavigateToHome : UiEvent()
    data class ShowToast(val message: String) : UiEvent()
}

class MyViewModel : ViewModel() {
    private val _uiEvent = MutableSharedFlow<UiEvent>()
    val uiEvent = _uiEvent.asSharedFlow()

    fun onLoginSuccess() {
        viewModelScope.launch {
            _uiEvent.emit(UiEvent.NavigateToHome)
        }
    }
}
Collecting in Activity or Compose:

kotlin
Copy
Edit
lifecycleScope.launchWhenStarted {
    viewModel.uiEvent.collect { event ->
        when (event) {
            is UiEvent.NavigateToHome -> navigateToHome()
            is UiEvent.ShowToast -> Toast.makeText(context, event.message, Toast.LENGTH_SHORT).show()
        }
    }
}
📌 Best Practices
Always expose SharedFlow as read-only using .asSharedFlow().

Use viewModelScope.launch to emit values safely.

Avoid replaying large values unless necessary.

Prefer SharedFlow over LiveData<Event> pattern (which often leads to sticky events).

In Jetpack Compose, remember to collect inside LaunchedEffect or rememberCoroutineScope.

❗ Common Pitfalls

Pitfall	Solution
No collectors? Emit is suspended.	Use extraBufferCapacity > 0 or tryEmit()
Multiple toasts/events firing again	Set replay = 0
Using for UI state	Prefer StateFlow instead
Lifecycle issues	Collect in lifecycleScope.launchWhenStarted
🧠 Final Thoughts
SharedFlow is a powerful addition to Kotlin’s reactive toolkit and fills a critical gap left by LiveData and StateFlow. It’s especially useful when you need event-based communication between ViewModel and UI, without worrying about lifecycle.