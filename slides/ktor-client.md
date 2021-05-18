#### RedditFeedApi

```kotlin [1-5|7-12|14-18|20-28|30-34|36|38-39]
@Serializable
data class RedditFeedResponse(
    val kind: String,
    val data: FeedData
)

@Serializable
data class FeedData(
    val modhash: String,
    val dist: Int,
    val children: List<RedditPost>
)

@Serializable
data class RedditPost(
    val kind: String,
    val data: RedditPostResponse
)

@Serializable
data class RedditPostResponse(
    val subreddit: String,
    val title: String,
    val subreddit_name_prefixed: String,
    val id: String
    val url: String
    val author: String
)

val client = HttpClient {
    install(JsonFeature) {
        serializer = KotlinxSerializer()
    }
}

class RedditFeedApi(private val httpClient: HttpClient) {

    suspend fun getDankMemes(): RedditFeedResponse =
        httpClient.get("https://www.reddit.com/r/dankmemes/.json")

}
```