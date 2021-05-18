#### Android 

```kotlin [2|3-7|8-10]
//in a fragment for simplicity
DI.repository.getDankMemes(
    onSuccess = { posts ->
        viewLifecycleOwner.lifecycleScope.launch(Dispatchers.Main) {
            adapter.submitList(posts as List<Post>)
        }
    },
    onError = {
        Log.e("FirstFragment", it.toString())
    }
)
```