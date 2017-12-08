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

val result = sum(1, 2)
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

```kotlin
// default arguments
fun read(b: Array<Byte>, off: Int = 0, len: Int = b.size) {
    // ...
}
```

```kotlin
fun foo(bar: Int = 0, baz: Int) {
    // ...
}

foo(baz = 1)
```

```kotlin
fun foo(bar: Int = 0, baz: Int = 1, qux: () -> Unit) {
    // ...
}

foo(1) { println("hello") } // default value baz = 1 
foo { println("hello") } // default values bar = 0 and baz = 1
```

```kotlin
fun reformat(str: String,
        normalizeCase: Boolean = true,
        upperCaseFirstLetter: Boolean = true,
        divideByCamelHumps: Boolean = false,
        wordSeparator: Char = ' ') {
    // ...
}

reformat(str)
reformat(str, true, true, false, '_')
reformat(str, wordSeparator = '_')
reformat(str,
    normalizeCase = true,
    upperCaseFirstLetter = true,
    divideByCamelHumps = false,
    wordSeparator = '_'
)
```

```kotlin
fun <T> asList(vararg ts: T): List<T> {
    val result = ArrayList<T>()
    for (t in ts)
        result.add(t)
    return result
}

val list = asList(1, 2, 3)

val a = arrayOf(1, 2, 3)
val list = asList(-1, 0, *a, 4)
```

```kotlin
infix fun Int.shl(x: Int): Int {
    // ...
}

1 shl 2
1.shl(2)
```

```kotlin
fun dfs(graph: Graph) {
    val visited = HashSet<Vertex>()
    fun dfs(current: Vertex) {
        if (!visited.add(current)) return
        for (v in current.neighbors)
            dfs(v)
    }

    dfs(graph.vertices[0])
}
```


Variables
=========

```kotlin
// read only
val a: Int = 1 // immediate assignment
val b = 2      // type is inferred
val c: Int     // no initializer
c = 3          // deferred assignment

// mutable
var x = 5
x += 1

// compile-time constant
const val TIMEOUT: Int = 30000
```


Null safety
===========

```kotlin
var x: String? = "abc"
x = null

val l: Int = if (x != null) x.length else -1

val l: Int? = x?.length

val l: Int = x?.length ?: -1
```

```kotlin
bob?.department?.head?.name
```

```kotlin
// return nullable value
fun parseInt(str: String): Int? {
    // ...
}
```

```kotlin
val l = b!!.length
```

```kotlin
value?.let {
    // execute this block if not null
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

```kotlin
val x: String = y as String
val x: String? = y as String?
val x: String? = y as? String
```

```kotlin
if (something is List<*>) {
    something.forEach { println(it) }
}
```

```kotlin
fun handleStrings(list: List<String>) {
    if (list is ArrayList) {
        // ...
    }
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

```kotlin
for (x in 1 until 10) {
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

```kotlin
println(map["key"])
map["key"] = value
```


Classes
=======

```kotlin
class Product {
}

val product = Product()
```

Constructor
-----------

```kotlin
class Person(name: String) {
    val personId = name.toUpperCase()

    init {
        println("Person initialized with value $name")
    }
}
```

```kotlin
class Person(val firstName: String, val lastName: String, var age: Int = 18) {
    // ...
}
```

```kotlin
class Person public @Inject constructor(name: String) {
    // ...
}
```

```kotlin
class DontCreateMe private constructor () {
    // ...
}
```

Secondary constructor
---------------------

```kotlin
class Person {
    constructor(name: String) {
        println("Person initialized with value $name")
    }
}
```

```kotlin
class Person(val name: String) {
    constructor(name: String, age: Int) : this(name) {
        println("Person initialized with value $name, $age")
    }
}
```

Inheritance
-----------

```kotlin
open class Base(p: Int)
class Derived(p: Int) : Base(p)
```

```kotlin
class MyView : View {
    constructor(ctx: Context) : super(ctx)
    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)
}
```

Override
--------

```kotlin
open class Base {
    open fun v() {}
    fun nv() {}
}

class Derived() : Base() {
    override fun v() {}
}

open class AnotherDerived() : Base() {
    final override fun v() {}
}
```

```kotlin
open class Foo {
    open val x: Int get() { ... }
}

class Bar1 : Foo() {
    override val x: Int = ...
}
```

```kotlin
interface Foo {
    val count: Int
}

class Bar1(override val count: Int) : Foo

class Bar2 : Foo {
    override var count: Int = 0
}
```

Abstract
--------

```kotlin
abstract class Product {
    abstract fun f()
}
```


Properties
==========

```kotlin
val isEmpty: Boolean
    get() = this.size == 0
```

```kotlin
var stringRepresentation: String
    get() = this.toString()
    set(value) {
        setDataFromString(value)
    }
```

```kotlin
var counter = 0
    set(value) {
        if (value >= 0) field = value
    }
```

```kotlin
lateinit var subject: TestSubject
```


Interfaces
==========

```kotlin
interface MyInterface {
    val prop: Int
    fun bar()
    fun foo() {
        // optional body
    }
}
```

```kotlin
class Child : MyInterface {
    override val prop: Int = 42
    override fun bar() {
        // body
    }
}
```


Visibility modifiers
====================

- private
- protected
- internal
- public (default)


Extensions
==========

```kotlin
fun MutableList<Int>.swap(index1: Int, index2: Int) {
    val tmp = this[index1]
    this[index1] = this[index2]
    this[index2] = tmp
}
```

```kotlin
fun Any?.toString(): String {
    if (this == null) return "null"
    return toString()
}
```

```kotlin
val <T> List<T>.lastIndex: Int
    get() = size - 1
```


Data classes
============

```kotlin
data class User(val name: String, val age: Int)
```


Sealed classes
==============

```kotlin
sealed class Expr
data class Const(val number: Double) : Expr()
data class Sum(val e1: Expr, val e2: Expr) : Expr()
object NotANumber : Expr()
```


Generics
========

```kotlin
class Box<T>(t: T) {
    var value = t
}
```

```kotlin
val box: Box<Int> = Box<Int>(1)
val box = Box(1)
```

Declaration-site variance
-------------------------

```kotlin
abstract class Source<out T> {
    abstract fun nextT(): T
}

fun demo(strs: Source<String>) {
    val objects: Source<Any> = strs
    // ...
}
```

```kotlin
abstract class Comparable<in T> {
    abstract fun compareTo(other: T): Int
}

fun demo(x: Comparable<Number>) {
    x.compareTo(1.0)
    val y: Comparable<Double> = x
}
```

Use-site variance: type projection
----------------------------------

```kotlin
fun copy(from: Array<out Any>, to: Array<Any>) {
    // ...
}
```

```kotlin
fun fill(dest: Array<in String>, value: String) {
    // ...
}
```

Star projection
---------------

For `interface Function<in T, out U>`:

- `Function<*, String>` means `Function<in Nothing, String>`
- `Function<Int, *>` means `Function<Int, out Any?>`
- `Function<*, *>` means `Function<in Nothing, out Any?>`

Generic functions
-----------------

```kotlin
fun <T> singletonList(item: T): List<T> {
    // ...
}
```

```kotlin
fun <T> T.basicToString() : String {
    // ...
}
```

```kotlin
val l = singletonList<Int>(1)
```

Generic constraints: upper bounds
---------------------------------

```kotlin
fun <T : Comparable<T>> sort(list: List<T>) {
    // ...
}
```


Nested and inner classes
========================

```kotlin
class Outer {
    private val bar: Int = 1
    class Nested {
        fun foo() = 2
    }
}

val demo = Outer.Nested().foo()
```

```kotlin
class Outer {
    private val bar: Int = 1
    inner class Inner {
        fun foo() = bar
    }
}

val demo = Outer().Inner().foo()
```

```kotlin
window.addMouseListener(object: MouseAdapter() {
    override fun mouseClicked(e: MouseEvent) {
        // ...
    }
                                                                                                            
    override fun mouseEntered(e: MouseEvent) {
        // ...
    }
})
```


Enum classes
============

```kotlin
enum class Direction {
    NORTH, SOUTH, WEST, EAST
}
```

```kotlin
enum class Color(val rgb: Int) {
        RED(0xFF0000),
        GREEN(0x00FF00),
        BLUE(0x0000FF)
}
```


Objects
=======

Object expressions
------------------

```kotlin
open class A(x: Int) {
    public open val y: Int = x
}

interface B { ... }

val ab: A = object : A(1), B {
    override val y = 15
}
```

```kotlin
fun foo() {
    val adHoc = object {
        var x: Int = 0
        var y: Int = 0
    }
    print(adHoc.x + adHoc.y)
}
```

```kotlin
fun countClicks(window: JComponent) {
    var clickCount = 0
    var enterCount = 0

    window.addMouseListener(object : MouseAdapter() {
        override fun mouseClicked(e: MouseEvent) {
            clickCount++
        }

        override fun mouseEntered(e: MouseEvent) {
            enterCount++
        }
    })
}
```

Object declarations
-------------------

```kotlin
object DataProviderManager {
    fun registerDataProvider(provider: DataProvider) {
        // ...
    }

    val allDataProviders: Collection<DataProvider>
        get() = // ...
}

DataProviderManager.registerDataProvider(...)
```

```kotlin
object DefaultListener : MouseAdapter() {
    override fun mouseClicked(e: MouseEvent) {
        // ...
    }

    override fun mouseEntered(e: MouseEvent) {
        // ...
    }
}
```

Companion objects
-----------------

```kotlin
class MyClass {
    companion object Factory {
        fun create(): MyClass = MyClass()
    }
}

val instance = MyClass.create()
```

```kotlin
class MyClass {
    companion object {
    }
}
```

```kotlin
interface Factory<T> {
    fun create(): T
}

class MyClass {
    companion object : Factory<MyClass> {
        override fun create(): MyClass = MyClass()
    }
}
```


Class delegation
================

```kotlin
interface Base {
    fun print()
}

class BaseImpl(val x: Int) : Base {
    override fun print() { print(x) }
}

class Derived(b: Base) : Base by b

fun main(args: Array<String>) {
    val b = BaseImpl(10)
    Derived(b).print()
}
```


Delegated properties
====================

```kotlin
class Example {
    var p: String by Delegate()
}

class Delegate {
    operator fun getValue(thisRef: Any?, property: KProperty<*>): String {
        return "$thisRef, thank you for delegating '${property.name}' to me!"
    }
 
    operator fun setValue(thisRef: Any?, property: KProperty<*>, value: String) {
        println("$value has been assigned to '${property.name} in $thisRef.'")
    }
}
```

```kotlin
val lazyValue: String by lazy {
    println("Computed!")
    "Hello"
}

fun main(args: Array<String>) {
    println(lazyValue)
    println(lazyValue)
}
```

```kotlin
class User {
    var name: String by Delegates.observable("<no name>") {
        prop, old, new ->
        println("$old -> $new")
    }
}

fun main(args: Array<String>) {
    val user = User()
    user.name = "first"
    user.name = "second"
}
```

```kotlin
class User(val map: Map<String, Any?>) {
    val name: String by map
    val age: Int     by map
}

fun main(args: Array<String>) {
    val user = User(mapOf(
        "name" to "John Doe",
        "age"  to 25
    ))
    println(user.name)
    println(user.age)
}
```

```kotlin
fun example(computeFoo: () -> Foo) {
    val memoizedFoo by lazy(computeFoo)
    if (someCondition && memoizedFoo.isValid()) {
        memoizedFoo.doSomething()
    }
}
```


Higher-order functions
======================

```kotlin
val sum = { x: Int, y: Int -> x + y }
```

```kotlin
val sum: (Int, Int) -> Int = { x, y -> x + y } // with optional type annotations
```

```kotlin
fun <T> lock(lock: Lock, body: () -> T): T {
    lock.lock()
    try {
        return body()
    }
    finally {
        lock.unlock()
    }
}

fun toBeSynchronized() = sharedResource.operation()
val result = lock(lock, ::toBeSynchronized)

val result = lock(lock, { sharedResource.operation() })

val result = lock (lock) {
    sharedResource.operation()
}
```

```kotlin
fun <T, R> List<T>.map(transform: (T) -> R): List<R> {
    val result = arrayListOf<R>()
    for (item in this)
        result.add(transform(item))
    return result
}

val doubled = ints.map { value -> value * 2 }

val doubled = ints.map { it * 2 }
```

```kotlin
strings
    .filter { it.length == 5 }
    .sortedBy { it }
    .map { it.toUpperCase() }
```

```kotlin
map.forEach { _, value -> println("$value!") }
```

```kotlin
fun <T> max(collection: Collection<T>, less: (T, T) -> Boolean): T? {
    var max: T? = null
    for (it in collection)
        if (max == null || less(max, it))
            max = it
    return max
}

max(strings, { a, b -> a.length < b.length })
```

```kotlin
val compare: (x: T, y: T) -> Int = ...
var sum: ((Int, Int) -> Int)? = null
```

Anonymous functions
-------------------

```kotlin
fun(x: Int, y: Int): Int = x + y
```

```kotlin
fun(x: Int, y: Int): Int {
    return x + y
}
```

```kotlin
ints.filter(fun(item) = item > 0)
```

Closures
--------

```kotlin
var sum = 0
ints.filter { it > 0 }.forEach {
    sum += it
}
print(sum)
```


Inline functions
================

```kotlin
inline fun <T> lock(lock: Lock, body: () -> T): T {
    // ...
}
```

```kotlin
inline fun foo(inlined: () -> Unit, noinline notInlined: () -> Unit) {
    // ...
}
```

```kotlin
inline fun <reified T> TreeNode.findParentOfType(): T? {
    var p = parent
    while (p != null && p !is T) {
        p = p.parent
    }
    return p as T?
}
```

```kotlin
inline fun <reified T> membersOf() = T::class.members

fun main(s: Array<String>) {
    println(membersOf<StringBuilder>().joinToString("\n"))
}
```


Destructuring declarations
==========================

```kotlin
val (name, age) = person

println(name)
println(age)
```

```kotlin
for ((a, b) in collection) { ... }
```

```kotlin
data class Result(val result: Int, val status: Status)
fun function(...): Result {
    // ...
    return Result(result, status)
}

val (result, status) = function(...)
```

```kotlin
for ((key, value) in map) {
   // ...
}
```

```kotlin
val (_, status) = getResult()
```

```kotlin
{ a -> ... } // one parameter
{ a, b -> ... } // two parameters
{ (a, b) -> ... } // a destructured pair
{ (a, b), c -> ... } // a destructured pair and another parameter
```


Equality
========

```kotlin
a === b // referential equality
a !== b // referential non-equality
a == b // structural equality
a != b // structural non-equality
```


Exceptions
==========

```kotlin
throw MyException("Hi There!")
```

```kotlin
try {
    // some code
}
catch (e: SomeException) {
    // handler
}
finally {
    // optional finally block
}
```

```kotlin
val a: Int? = try { parseInt(input) } catch (e: NumberFormatException) { null }
```

```kotlin
fun fail(message: String): Nothing {
    throw IllegalArgumentException(message)
}
```


Type aliases
============

```kotlin
typealias NodeSet = Set<Network.Node>
typealias FileTable<K> = MutableMap<K, MutableList<File>>
```

```kotlin
typealias MyHandler = (Int, String, Any) -> Unit
typealias Predicate<T> = (T) -> Boolean
```

```kotlin
class A {
    inner class Inner
}
class B {
    inner class Inner
}

typealias AInner = A.Inner
typealias BInner = B.Inner
```
