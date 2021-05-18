#### Creating the database 

```kotlin [1-2|4-10|12-16|18-21]
// in src/commonMain/kotlin
expect fun createDb(): MyDatabase

// in src/androidMain/kotlin
lateinit var context: Context

actual fun createDb(): MyDatabase {
    val driver = AndroidSqliteDriver(MyDatabase.Schema, context, "test.db")
    return MyDatabase.invoke(driver)
}

// in src/nativeMain/kotlin
actual fun createDb(): MyDatabase {
    val driver = NativeSqliteDriver(MyDatabase.Schema, "test.db")
    return MyDatabase.invoke(driver)
}

//in src/jsMain/kotlin
actual fun createDb(): MyDatabase {
    TODO("JS does not need to persist data")
}
```