---
layout: post
title: "📡Android different serialization techniques"
author: anil
categories: [Kotlin, Android, Architecture]
tags: [Serialization, Android Networking]
image: data:image/png;base64,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
featured: false
---
# 🥊 Gson vs Moshi vs kotlinx.serialization: The Ultimate JSON Showdown in Android

In Android development, JSON parsing is an everyday task. Whether you’re fetching API data or persisting state, choosing the right serialization library is crucial.

The three most popular contenders are:
- **Gson**: The old-school favorite by Google
- **Moshi**: A modern, reflection-free solution by Square
- **kotlinx.serialization**: Kotlin's own type-safe, multiplatform-first library

Let’s compare them in terms of performance, syntax, flexibility, and use cases.

---

## 🧬 TL;DR Comparison Table

| Feature                        | Gson             | Moshi            | kotlinx.serialization   |
|-------------------------------|------------------|------------------|--------------------------|
| Kotlin-first                  | ❌               | ⚠️ Partial       | ✅                      |
| Reflection-free               | ❌               | ✅ (with adapters) | ✅                      |
| Annotation style              | Java-style       | Cleaner Kotlin   | Native Kotlin            |
| Default value support         | ❌               | ✅               | ✅                      |
| Custom serializers            | ✅               | ✅               | ✅                      |
| Built-in null safety          | ❌               | ✅               | ✅                      |
| Multiplatform support         | ❌               | ❌               | ✅                      |
| Retrofit integration          | ✅               | ✅               | ⚠️ (requires converter)  |
| Performance                   | Moderate         | High             | Very High                |

---

## 🧪 1. Gson

**Developed by:** Google  
**Maturity:** Very mature, long-standing  
**Reflection-based:** Yes (uses `java.lang.reflect`)  
**Pros:**
- Simple API
- Widely used, well-documented
- Supported out-of-the-box in Retrofit

**Cons:**
- Slower due to reflection
- No native Kotlin support (no default values, null safety)
- Can't handle Kotlin-specific features like `val`/`var` well

### Example

```kotlin
data class User(val name: String, val age: Int)
val gson = Gson()
val json = gson.toJson(User("Alice", 25))
val user = gson.fromJson(json, User::class.java)
```
⚡ 2. Moshi
Developed by: Square
Reflection-free: Yes (when using KotlinJsonAdapterFactory)
Kotlin Support: Good (but not native)

Pros:

No reflection if you use code-gen

Supports custom adapters and annotations

Works great with Retrofit

Safer handling of nulls and default values

Cons:

Kotlin support requires kapt/code-gen setup

More boilerplate for custom adapters

Example
```
@JsonClass(generateAdapter = true)
data class User(val name: String, val age: Int)

val moshi = Moshi.Builder()
    .add(KotlinJsonAdapterFactory())
    .build()

val adapter = moshi.adapter(User::class.java)
val json = adapter.toJson(User("Alice", 25))
val user = adapter.fromJson(json)
```
🌐 3. kotlinx.serialization

Developed by: JetBrains
Kotlin-native: ✅
Reflection-free: ✅
Multiplatform support: ✅

Pros:

Compile-time safety

Native Kotlin syntax

Fast and lightweight

Works in Kotlin Multiplatform (JVM, JS, Native)

Great for modern Android development

Cons:

Retrofit doesn’t support it out-of-the-box

Custom serialization can be verbose

Example
kotlin
Copy
Edit
@Serializable
data class User(val name: String, val age: Int)

val json = Json.encodeToString(User("Alice", 25))
val user = Json.decodeFromString<User>(json)
🧩 Use Cases

Use Case	Recommended Library
Legacy projects with Gson	✅ Stick with Gson
New Android app with Retrofit	✅ Moshi or kotlinx.serialization
Kotlin Multiplatform (KMM)	✅ kotlinx.serialization
Performance-critical apps	✅ kotlinx.serialization
Need for full JSON flexibility	✅ Moshi
🔄 Retrofit Integration

Library	Retrofit Support
Gson	✅ Native
Moshi	✅ Native
kotlinx.serialization	⚠️ Via retrofit-kotlinx-serialization-converter
✅ Summary
Use Gson if you’re maintaining a legacy codebase or need simplicity.

Choose Moshi for most Android apps — it's fast, safe, and works great with Retrofit.

Go with kotlinx.serialization if:

You’re building with Kotlin Multiplatform

You want full compile-time safety

You value performance and Kotlin idioms

🧠 Final Thoughts
Choosing the right serialization tool depends on your project goals, platform requirements, and team preferences. While Gson still works, Moshi and kotlinx.serialization are the future — especially in modern Android and Kotlin-first environments.