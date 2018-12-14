#### Intercepting Filter Pattern

Recently after playing around with WebFlux Spring Security, I realised it was based on a J2EE Intercepting Filter Pattern used in the presentation layer.    

**Problem**: You want to intercept and manipulate a request and a response before and after the request is processed.

**Solution**: Use an Intercepting Filter as a pluggable filter to pre and postprocess requests and responses. A filter manager combines loosely coupled filters in a chain, delegating control to the appropriate filter. In this way, you can add, remove, and combine these filters in various ways without changing existing code

![UML Diagram](http://www.corej2eepatterns.com/images/IFMainClass.gif)

Usefull Resources: 

- [Intercepting Filter Pattern in Java](https://www.baeldung.com/intercepting-filter-pattern-in-java)
- [Core J2EE Patterns](http://www.corej2eepatterns.com/InterceptingFilter.htm)
- [Wikipedia](https://en.wikipedia.org/wiki/Intercepting_filter_pattern)


```kotlin
interface Filter {
    fun execute(request: String)
}
```

```kotlin
data class Target(private val process: (String) -> Unit) {
    fun execute(request: String) =
        process.invoke(request)
}
```

```kotlin
class LogFilter : Filter {
    override fun execute(request: String) =
        println(request)
}
```

```kotlin
data class FilterChain(
    private val target: Target,
    private val filters: List<Filter> = listOf()) : Filter {

    fun with(filter: Filter) =
        copy(filters = this.filters + listOf(filter))

    override fun execute(request: String) {
        filters.forEach { it.execute(request) }
            .let { target.execute(request) }
        }
}
```

```kotlin
data class FilterManager(
    private val target: Target,
    private val chain: FilterChain = FilterChain(target)) {

    fun with(filter: Filter) = copy(chain = chain.with(filter))

    fun execute(request: String) = chain.execute(request)
}
```

```kotlin
fun main(args: Array<String>) {
    val target = Target { it -> println(it.toUpperCase())}
    FilterManager(target)
        .with(filter = LogFilter())
        .execute("Test")
}
```

