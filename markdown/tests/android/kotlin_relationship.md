:::NEW_COMMAND:::
:::ONE_TO_ONE:::

Example: **One post** (source model) has **one author** (target model).

**Create**

In order to save a 1:1 relationship, create the target model instance first and then save it to the source model instance.

```kotlin
val newAuthor = Author.builder()
    .name("Rene Brandel")
    .build()
val post = Post.builder()
    .content("My first post!")
    .author(newAuthor)
    .build()

Amplify.DataStore.save(newAuthor,
    {
        Amplify.DataStore.save(post,
            { Log.i("DataStore", "Post saved") },
            { Log.e("DataStore", "Failed to save post", it) }
        )
    },
    { Log.e("DataStore", "Failed to save author", it) }
)
```
Here we've first created a new `Author` instance and then saved it to the `Post`'s "author" relationship field.

**Query**

To query one-to-one relationships, access the target model instance through its source model instance's field.

```kotlin
Amplify.DataStore.query(Post::class.java,
    { matchingPosts ->
        while (matchingPosts.hasNext()) {
            Log.i("DataStore", "Author: ${matchingPosts.next().author}")
        }
    },
    { Log.e("DataStore", "Failed to query", it) }
)
```

**Delete**

In one-to-one relationships, if the target model instance is deleted, it will also clear the source model instance's relationship field.

```kotlin
Amplify.DataStore.delete(newAuthor,
    { Log.i("DataStore", "Author + Post deleted") },
    { Log.e("DataStore", "Deletion failed", it) }
)
```

In this example, the `Post`'s "author" field will be cleared and the `Author` model instance will be deleted.

:::NEW_COMMAND:::
:::ONE_TO_MANY:::

Example: **One publication** (source model) has **many articles** (target model)

**Create**

In order to save a one-to-many relationship, create the source model instance first and then save its _id_ to the target model instance's relationship source field.

```kotlin
val publication = Publication.builder()
    .title("Amplify Weekly")
    .build()

val article = Article.builder()
    .publicationId(publication.getId())
    .title("Add auth to your app in 3 steps")
    .build()

Amplify.DataStore.save(publication,
    {
        Amplify.DataStore.save(article,
            { Log.i("DataStore", "Article saved: $it") },
            { Log.e("DataStore", "Failed to save article", it) }
        )
    },
    { Log.e("DataStore", "Failed to save publication", it) }
)
```
Here we've first created a new `Publication` instance and then saved its _id_ to the `Article`'s "publicationID" relationship field.

**Query**

To query one-to-many relationships, filter based on the source model instance's id on the target model.

```kotlin
val conditions = Article.PUBLICATION_ID.eq("YOUR_PUBLICATION_ID")
Amplify.DataStore.query(Article::class.java, Where.matches(conditions),
    { articleMatches ->
        while (articleMatches.hasNext()) {
            Log.i("DataStore", "Matched article: ${articleMatches.next()}")
        }
    },
    { Log.e("DataStore", "Query failed", it) }
)
```

**Delete**

In one-to-many relationships, delete the target model instance first and then delete the source model.

```kotlin
val conditions = Article.PUBLICATION_ID.eq("YOUR_PUBLICATION_ID")
Amplify.DataStore.query(Article::class.java, Where.matches(conditions),
    { matchingArticles ->
        while (matchingArticles.hasNext()) {
            Amplify.DataStore.delete(matchingArticles.next()!!,
                { Log.i("DataStore", "Article deleted") },
                { Log.e("DataStore", "Deletion failed", it) }
            )
        }
        Amplify.DataStore.query(Publication::class.java, Where.id("YOUR_PUBLICATION_ID"),
            { matchingPublications ->
                while (matchingPublications.hasNext()) {
                    Amplify.DataStore.delete(matchingPublications.next(),
                        { Log.i("DataStore", "Publication deleted") },
                        { Log.e("DataStore", "Deletion failed", it) }
                    )
                }
            },
            { Log.e("DataStore", "Query failed", it) }
        )
    },
    { Log.e("DataStore", "Query failed", it) }
)
```

In this example, the `Publication` with "YOUR_PUBLICATION_ID" and all of its related `Article` model instances will be deleted.

:::NEW_COMMAND:::
:::MANY_TO_MANY:::

Example: **Posts** have **many tags** and **Tags** have **many posts**. 

In any many-to-many relationship, Amplify admin UI automatically creates a "join model" consisting of the combination of the source model names. In our example, Amplify automatically creates a **PostTag** join model.

**Create**

In order to save a many-to-many relationship, create both model instance first and then save them to a new join model instance.

```kotlin
val post = Post.builder()
    .body("How to build deploy a web app on AWS Amplify")
    .build()

val tag = Tag.builder()
    .label("static-web-hosting")
    .build()

val postTag = PostTag.builder()
    .post(post)
    .tag(tag)
    .build()

Amplify.DataStore.save(post,
    { postSaved ->
        Log.i("DataStore", "Post saved")
        Amplify.DataStore.save(tag,
            { tagSaved ->
                Log.i("DataStore", "Tag saved")
                Amplify.DataStore.save(postTag,
                    { Log.i("DataStore", "PostTag saved") },
                    { Log.e("DataStore", "Failed to save PostTag", it) }
                )
            },
            { Log.e("DataStore", "Failed to save Tag", it) }
        )
    },
    { Log.e("DataStore", "Failed to save Post", it) }
)
```

Here we've first created a new `Post` instance and a new `Tag` instance. Then, saved those instances to a new instance of our join model `PostTag`.

**Query**

To query many-to-many relationships, filter the join model based on one of the model's _id_.

```kotlin
val conditions = ContentTag.CONTENT.eq("YOUR_CONTENT_ID")
Amplify.DataStore.query(ContentTag::class.java, Where.matches(conditions),
    { matchingContentTags ->
        while (matchingContentTags.hasNext()) {
            Log.i("DataStore", "Tag: ${matchingContentTags.next().tag}")
        }
    },
    { Log.e("DataStore", "Query failed", it) }
)
```

In this example, first filter the _join model_ `PostTag` with your `Post`'s _id, then map the `PostTag`s to `Tag`s.

**Delete**

Deleting the _join model instance_ will not delete any source model instances.

```kotlin
Amplify.DataStore.delete(toBeDeletedPostTag,
    { Log.i("DataStore", "Deleted $toBeDeletedPostTag") },
    { Log.e("DataStore", "Deletion failed", it) }
)
```
Both the `Post` and the `Tag` instances will not be deleted. Only the join model instances containing the link between a `Post` and a `Tag`.  

Deleting a _source model instance_ will also delete the join model instances containing the source model instance.
```kotlin
Amplify.DataStore.delete(toBeDeletedTag,
    { Log.i("DataStore", "Deleted $toBeDeletedTag") },
    { Log.e("DataStore", "Deletion failed", it) }
)
```
The `toBeDeletedTag` `Tag` instance and all `PostTag` instances where _tag_ is linked to `toBeDeletedTag` will be deleted.
