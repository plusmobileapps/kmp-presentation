### Post.sq file

```[3-11|13-23|25-26]
import kotlinx.serialization.PrimitiveKind.INT;

CREATE TABLE Post(
id TEXT NOT NULL PRIMARY KEY,
title TEXT NOT NULL,
subreddit_name_prefixed TEXT NOT NULL,
downs INTEGER as Int,
ups INTEGER as Int,
url TEXT NOT NULL,
author TEXT NOT NULL,
);

insertItem:
INSERT OR REPLACE INTO Post(
    id, 
    title, 
    subreddit_name_prefixed,
    downs, 
    ups, 
    url, 
    author
)
VALUES(?,?,?,?,?,?,?);

selectAll:
SELECT * FROM Post;
```