:::NEW_COMMAND:::
:::ONE_TO_ONE:::

Example: **One post** (source model) has **one author** (target model).

**Create**

In order to save a 1:1 relationship, create the target model instance first and then save it to the source model instance.

```java
Author newAuthor = Author.builder()
    .name("Rene Brandel")
    .build();
Post post = Post.builder()
    .content("My first post!")
    .author(newAuthor)
    .build();

Amplify.DataStore.save(newAuthor,
    authorSaved -> {
        Amplify.DataStore.save(post,
            postSaved -> Log.i("DataStore", "Post saved"),
            postSaveFailure ->
                Log.e("DataStore", "Failed to save post:", postSaveFailure)
        );
    },
    authorSaveFailure ->
        Log.e("DataStore", "Failed to save author:", authorSaveFailure)
);
```
Here we've first created a new `Author` instance and then saved it to the `Post`'s "author" relationship field.

**Query**

To query one-to-one relationships, access the target model instance through its source model instance's field.

```java
Amplify.DataStore.query(Post.class,
    matchingPosts -> {
        while (matchingPosts.hasNext()) {
            Post post = matchingPosts.next();
            Author author = post.getAuthor();
            Log.i("DataStore", "Author: " + author.toString());
        }
    },
    failure -> Log.e("DataStore", "Query failed", failure)
);
```

**Delete**

In one-to-one relationships, if the target model instance is deleted, it will also clear the source model instance's relationship field.

```java
Amplify.DataStore.delete(author,
    success -> Log.i("DataStore", "Author + Post deleted"),
    failure -> Log.e("DataStore", "Deletion failed", failure)
);
```

In this example, the `Post`'s "author" field will be cleared and the `Author` model instance will be deleted.

:::NEW_COMMAND:::
:::ONE_TO_MANY:::

Example: **One publication** (source model) has **many articles** (target model)

**Create**

In order to save a one-to-many relationship, create the source model instance first and then save its _id_ to the target model instance's relationship source field.

```java
Publication publication = Publication.builder()
    .title("Amplify Weekly")
    .build();

Article article = Article.builder()
    .publicationId(publication.getId())
    .title("Add auth to your app in 3 steps")
    .build();

Amplify.DataStore.save(publication,
    pubSaved -> {
        Amplify.DataStore.save(article,
            articleSaved -> Log.i("DataStore", "Article saved"),
            articleSaveFailure ->
                Log.e("DataStore", "Failed to save article", articleSaveFailure)
        );
    },
    pubSaveFailure -> Log.e("DataStore", "Error while saving:", pubSaveFailure)
);
```
Here we've first created a new `Publication` instance and then saved its _id_ to the `Article`'s "publicationID" relationship field.

**Query**

To query one-to-many relationships, filter based on the source model instance's id on the target model.

```java
QueryPredicate conditions = Article.PUBLICATION_ID.eq("YOUR_PUBLICATION_ID")
Amplify.DataStore.query(Article.class, Where.matches(conditions),
    matchingArticles -> {
        while (matchingArticles.hasNext()) {
            Article article = matchingArticles.next();
            Log.i("DataStore", "Matched article: " + article);
        }
    },
    failure -> Log.e("DataStore", "Query failed", failure)
);
```

**Delete**

In one-to-many relationships, delete the target model instance first and then delete the source model.

```java
QueryPredicate conditions = Article.PUBLICATION_ID.eq("YOUR_PUBLICATION_ID");
Amplify.DataStore.query(Article.class, Where.matches(conditions),
    matchingArticles -> {
        while (matchingArticles.hasNext()) {
            Article article = matchingArticles.next();
            Amplify.DataStore.delete(article,
                articleDeleted -> Log.i("DataStore", "Article deleted"),
                articleDeletionFailure ->
                    Log.e("DataStore", "Failed to delete article", articleDeletionFailure)
            );
        }
        Amplify.DataStore.query(Publication.class, Where.id("YOUR_PUBLICATION_ID"),
            matchingPubs -> {
                while (matchingPubs.hasNext()) {
                    Publication publication = matchingPubs.next();
                    Amplify.DataStore.delete(publication,
                        pubDeleted -> Log.i("DataStore", "Publication deleted"),
                        pubDeletionFailure ->
                            Log.e("DataStore", "Failed to delete publication", pubDeletionFailure)
                    );
                }
            },
            pubQueryFailure -> Log.e("DataStore", "Failed to query publications", pubQueryFailure)
        );
    },
    articleQueryFailure -> Log.e("DataStore", "Failed to query articles", articleQueryFailure)
);
```

In this example, the `Publication` with "YOUR_PUBLICATION_ID" and all of its related `Article` model instances will be deleted.

:::NEW_COMMAND:::
:::MANY_TO_MANY:::

Example: **Posts** have **many tags** and **Tags** have **many posts**. 

In any many-to-many relationship, Amplify admin UI automatically creates a "join model" consisting of the combination of the source model names. In our example, Amplify automatically creates a **PostTag** join model.

**Create**

In order to save a many-to-many relationship, create both model instance first and then save them to a new join model instance.

```java
Post post = Post.builder()
    .body("How to build deploy a web app on AWS Amplify")
    .build();

Tag tag = Tag.builder()
    .label("static-web-hosting")
    .build();

PostTag postTag = PostTag.builder()
    .post(post)
    .tag(tag)
    .build();

Amplify.DataStore.save(post,
    postSaved -> {
        Log.i("DataStore", "Post saved");
        Amplify.DataStore.save(tag,
            tagSaved -> {
                Log.i("DataStore", "Tag saved");
                Amplify.DataStore.save(postTag,
                    postTagSaved -> Log.i("DataStore", "PostTag saved"),
                    postTagSaveFailure ->
                        Log.e("DataStore", "PostTag not saved", postTagSaveFailure)
                );
            },
            tagSaveFailure ->
                Log.e("DataStore", "Tag not saved", tagSaveFailure)
        );
    },
    postSaveFailure -> Log.e("DataStore", "Post not saved", postSaveFailure)
);
```

Here we've first created a new `Post` instance and a new `Tag` instance. Then, saved those instances to a new instance of our join model `PostTag`.

**Query**

To query many-to-many relationships, filter the join model based on one of the model's _id_.

```java

QueryPredicate conditions = ContentTag.CONTENT.eq("YOUR_CONTENT_ID");
Amplify.DataStore.query(ContentTag.class, Where.matches(conditions)),
    matchingContentTags -> {
        while (matchingContentTags.hasNext()) {
            ContentTag contentTag = matchingContentTags.next();
            Log.i("DataStore", "Tag: " + contentTag.getTag());
        }
    },
    failure -> Log.e("DataStore", "Failed to query ContentTags", failure)
);
```

In this example, first filter the _join model_ `PostTag` with your `Post`'s _id, then map the `PostTag`s to `Tag`s.

**Delete**

Deleting the _join model instance_ will not delete any source model instances.

```java
Amplify.DataStore.delete(toBeDeletedPostTag,
    success -> Log.i("DataStore", "PostTag deleted"),
    failure -> Log.e("DataStore", "Deletion failed", failure)
);
```
Both the `Post` and the `Tag` instances will not be deleted. Only the join model instances containing the link between a `Post` and a `Tag`.  

Deleting a _source model instance_ will also delete the join model instances containing the source model instance.
```java
Amplify.DataStore.delete(toBeDeletedTag,
    success -> Log.i("DataStore", "PostTag deleted"),
    failure -> Log.e("DataStore", "Deletion failed", failure)
);

```
The `toBeDeletedTag` `Tag` instance and all `PostTag` instances where _tag_ is linked to `toBeDeletedTag` will be deleted.
