#### Dependency Injection

```kotlin [1|3|4|5-9|10|11-15]
expect val ioDispatcher: CoroutineDispatcher 

object DI {
    private val database: MyDatabase = createDb() 
    private val client = HttpClient {
        install(JsonFeature) {
            serializer = KotlinxSerializer()
        }
    }
    val api = RedditFeedApi(client)
    val repository = FeedRepository(
        db = database, 
        api = api, 
        dispatcher = ioDispatcher
    )
}
```