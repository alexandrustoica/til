# Visitor Design Pattern

<br>

> The visitor design pattern is a way of separating an algorithm from an object structure on which it operates. A practical result of this separation is the ability to add new operations to existent object structures without modifying the structures. It is one way to follow the open/closed principle.

<img src="https://upload.wikimedia.org/wikipedia/en/thumb/e/eb/Visitor_design_pattern.svg/1920px-Visitor_design_pattern.svg.png" width="500">

<br>

```kotlin
interface StoreItem {
    fun accept(visitor: StoreVisitor): Unit
	fun price(): Int
}
```

<br>

```kotlin
data class Book(private val price: Int = 100): StoreItem {
    
    override fun accept(visitor: StoreVisitor): Unit =
        visitor.visit(this)
    
    override fun price() = this.price
}
```

<br>

```kotlin
data class Candy(private val price: Int = 10): StoreItem {
    
    override fun accept(visitor: StoreVisitor): Unit =
       	visitor.visit(this)
    
    override fun price() = this.price
}
```

<br>

```kotlin
interface StoreVisitor {
    fun visit(item: StoreItem): Unit
    fun total(): Int
}
```

<br>

```kotlin
class AuchanVisitor: StoreVisitor {
    private var total: Int = 0
    private val tax: (Int) -> Int = {it -> (it * 3.4 / 100).toInt()}
    
    override fun visit(item: StoreItem): Unit {
        this.total += item.price() + tax(item.price())
    }
    
    override fun total() = this.total
}
```

<br>

```kotlin
fun main() {
    val auchan = AuchanVisitor()
    val items = listOf(Book(price = 120), Candy(price = 20))
    items.forEach { it.accept(auchan) }
    println(auchan.total())
}
```
