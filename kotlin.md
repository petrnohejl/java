Kotlin
======


Comments
========

```kotlin
// This is an end-of-line comment

/* This is a block comment
   on multiple lines. */
```


Packages
========

```kotlin
package com.example

import foo.Bar
```


Functions
=========

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

```kotlin
// expression body and inferred return type
fun sum(a: Int, b: Int) = a + b
```

```kotlin
// no return value
fun printSum(a: Int, b: Int): Unit {
    println("sum of $a and $b is ${a + b}")
}
```

```kotlin
// omitted Unit
fun printSum(a: Int, b: Int) {
    println("sum of $a and $b is ${a + b}")
}
```


Variables
=========

Read only variable
------------------

```kotlin
val a: Int = 1 // immediate assignment
val b = 2      // type is inferred
val c: Int     // no initializer
c = 3          // deferred assignment
```

Mutable variable
----------------

```kotlin
var x = 5
x += 1
```


String templates
================

```kotlin
var a = 1
val s1 = "a is $a" 

a = 2
val s2 = "${s1.replace("is", "was")}, but now is $a"
```


Conditional expressions
=======================

If
--

```kotlin
fun maxOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    } else {
        return b
    }
}
```

```kotlin
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```

When
----

```kotlin
fun describe(obj: Any): String =
when (obj) {
    1          -> "One"
    "Hello"    -> "Greeting"
    is Long    -> "Long"
    !is String -> "Not a string"
    else       -> "Unknown"
}
```


Null safety
===========

```kotlin
// return nullable value
fun parseInt(str: String): Int? {
    // ...
}
```


Type casts
==========

```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj is String) {
        // obj is automatically cast to String in this branch
        return obj.length
    }

    return null
}
```

```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj !is String) return null

    // obj is automatically cast to String in this branch
    return obj.length
}
```


Loops
=====

For
---

```kotlin
val items = listOf("apple", "banana", "kiwi")
for (item in items) {
    println(item)
}
```

```kotlin
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}
```

While
-----

```kotlin
val items = listOf("apple", "banana", "kiwi")
var index = 0
while (index < items.size) {
    println("item at $index is ${items[index]}")
    index++
}
```


Ranges
======

```kotlin
val x = 10
val y = 9
if (x in 1..y+1) {
    println("fits in range")
}
```

```kotlin
for (x in 1..5) {
    print(x)
}
```

```kotlin
for (x in 1..10 step 2) {
    print(x)
}
```

```kotlin
for (x in 9 downTo 0 step 3) {
    print(x)
}
```


Collections
===========

```kotlin
for (item in items) {
    println(item)
}
```

```kotlin
when {
    "orange" in items -> println("juicy")
    "apple" in items -> println("apple is fine too")
}
```

```kotlin
fruits
    .filter { it.startsWith("a") }
    .sortedBy { it }
    .map { it.toUpperCase() }
    .forEach { println(it) }
```
