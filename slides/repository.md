#### Repository

```kotlin [1-5|7-8|10|11-15|16|18|19-20|38-46|21-28|31|32-34]
class FeedRepository(
    private val db: MyDatabase,
    private val api: RedditFeedApi,
    dispatcher: CoroutineDispatcher
) {

    private val job = Job()
    private val scope = CoroutineScope(job + dispatcher)

    fun getDankMemes(onSuccess: (List<Post>) -> Unit, onError: (Any) -> Unit) {
        val cache = db.postQueries.selectAll().executeAsList()
        if (cache.isNotEmpty()) {
            onSuccess(cache)
            return
        }
        scope.launch {
            try {
                val response = api.getDankMemes()
                val posts = response.data.children.map { redditPost ->
                    val post = redditPost.toPost()
                    db.postQueries.insertItem(
                        id = post.id,
                        url = post.url,
                        permalink = post.permalink,
                        author = post.author,
                        subreddit = post.subreddit,
                        title = post.title
                    )
                    post
                }
                onSuccess(posts)
            } catch (e: Exception) {
                onError(e)
            }
        }
    }

    private fun RedditPost.toPost(): Post {
        return Post(
            id = data.id,
            title = data.title,
            subreddit = data.subreddit,
            author = data.author,
            url = data.url
        )
    }

}
```