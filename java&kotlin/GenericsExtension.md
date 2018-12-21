#### Generic Extension Methods

Extension methods can be applied to a generic receiver as well as a concrete one.

```kotlin
fun <A, Monad> A.bind(f: (A) -> Monad): Monad =
    this.also { println("$it") }.let(f)
```
```kotlin
fun <A, B> A.concat(other: B): String = 
    this.toString() + other.toString()
```

```kotlin   

(4 + 5).bind { lhs ->       // 9
    (6 - 9).bind { rhs ->   // -3
        print(lhs + rhs)    // 6
    }
}

println("2".concat(3))      // 23
```
