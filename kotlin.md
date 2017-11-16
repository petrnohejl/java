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
import moo.*
import boo.Bar as bBar
```


Types
=====

Numbers
-------

- Double
- Float
- Long
- Int
- Short
- Byte

```kotlin
123L // long
0x0F // hexadecimal
0b00001011 // binary
123.5F // float
```

```kotlin
// underscores in numeric literals
1_000_000
1234_5678_9012_3456L
0xFF_EC_DE_5E
0b11010010_01101001_10010100_10010010
```

Arrays
------

```kotlin
val a = arrayOf(1, 2, 3)
val b = intArrayOf(1, 2, 3)
val c: Array<Int?> = arrayOfNulls(8)
val d: Array<String> = Array(8, { it.toString() })
a[0] = a[1] + a[2]
```

String
------

```kotlin
val s = "Hello, world!\n"

val text = """
|Tell me and I forget.
|Teach me and I remember.
|Involve me and I learn.
|(Benjamin Franklin)
""".trimMargin()
```

String templates
----------------

```kotlin
var a = 1
val s1 = "a is $a" 

a = 2
val s2 = "${s1.replace("is", "was")}, but now is $a"
```

Other
-----

```kotlin
val b: Boolean = true
val c: Char = '8'
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

val max = if (a > b) {
    print("Choose a")
    a
} else {
    print("Choose b")
    b
}
```

When
----

```kotlin
when (x) {
    0, 1 -> print("x == 0 or x == 1")
    2 -> print("x == 2")
    else -> {
        print("x is neither 1 nor 2")
    }
}
```

```kotlin
fun describe(obj: Any): String =
when (obj) {
    0          -> "Zero"
    in 1..9    -> "Numero"
    "Hello"    -> "Greeting"
    is Long    -> "Long"
    !is String -> "Not a string"
    else       -> "Unknown"
}
```

```kotlin
when {
    x.isOdd() -> print("x is odd")
    x.isEven() -> print("x is even")
    else -> print("x is funny")
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

```kotlin
for ((index, value) in array.withIndex()) {
    println("the element at $index is $value")
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

```kotlin
do {
    val y = retrieveData()
} while (y != null)
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
