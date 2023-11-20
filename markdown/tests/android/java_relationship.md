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
    savedAuthor -> {
        Amplify.DataStore.save(post,
            savedPost -> Log.i("Amplify DataStore", "Post saved."),
            failure -> Log.e("Amplify DataStore", "Error while saving:", failure)
        );
    },
    failure -> Log.e("Amplify DataStore", "Error while saving:", failure)
);
```
Here we've first created a new `Author` instance and then saved it to the `Post`'s "author" relationship field.

**Query**

To query one-to-one relationships, access the target model instance through its source model instance's field.

```java
Amplify.DataStore.query(Post.class,
    matches -> {
        while (matches.hasNext()) {
            Post post = matches.next();
            Author author = post.getAuthor();
        }
    },
    failure -> Log.e("Amplify DataStore", "Query failed.", failure)
);
```

**Delete**

In one-to-one relationships, if the target model instance is deleted, it will also clear the source model instance's relationship field.

```java
Amplify.DataStore.delete(author,
    deleted -> Log.i("Amplify DataStore", "Author deleted."),
    failure -> Log.e("Amplify DataStore", "Deletion failed", failure));
```

In this example, the `Post`'s "author" field will be cleared and the `Author` model instance will be deleted.

If the source model is deleted, the target model will be automatically deleted as well.  

```java
Amplify.DataStore.delete(post,
    deleted -> Log.i("Amplify DataStore", "Author + Post deleted"),
    failure -> Log.e("Amplify DataStore", "Deletion failed", failure));
```

In this example, the `Post` model instance will be deleted and the `Author` model instance will be deleted, locally, and on the backend.

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
    savedPublication -> {
        Amplify.DataStore.save(article,
            savedArticle -> Log.i("Amplify DataStore", "Article saved." + savedArticle),
            failure -> Log.e("Amplify DataStore", "Error while saving:", failure)
        );
    },
    failure -> Log.e("Amplify DataStore", "Error while saving:", failure)
);
```
Here we've first created a new `Publication` instance and then saved its _id_ to the `Article`'s "publicationID" relationship field.

**Query**

To query one-to-many relationships, filter based on the source model instance's id on the target model.

```java
Amplify.DataStore.query(Article.class, Where.matches(Article.PUBLICATION_ID.eq("YOUR_PUBLICATION_ID")),
    matches -> {
        while(matches.hasNext()) {
            Article article = matches.next();
            Log.i("Amplify DataStore", "Matched article: " + article);
        }
    },
    failure -> Log.e("Amplify DataStore", "Query failed.", failure));
```

**Delete**

In one-to-many relationships, deleting the source model will automatically delete all target models that belong to it, both locally, and on the backend.

```java
Amplify.DataStore.query(Publication.class, Where.id("YOUR_PUBLICATION_ID"),
    matchedPublications -> {
        while (matchedPublications.hasNext()) {
            Publication match = matchedPublications.next();
            Amplify.DataStore.delete(match,
                deleted -> Log.i("Amplify DataStore", "Publication and all related Article instances deleted"),
                failure -> Log.e("Amplify DataStore", "Deletion failed.", failure));
        }
    },
    failure -> {}
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
        savedPost -> {
        Log.i("Amplify DataStore", "post saved.");
        Amplify.DataStore.save(tag,
            savedEditor -> {
                Log.i("Amplify DataStore", "Tag saved.");
                Amplify.DataStore.save(postTag,
                    saved -> Log.i("Amplify DataStore", "PostTag saved."),
                    failure -> Log.e("Amplify DataStore", "PostTag not saved.", failure)
                );
            },
            failure -> Log.e("Amplify DataStore", "Tag not saved.", failure)
        );
    },
    failure -> Log.e("Amplify DataStore", "Post not saved.", failure)
);
```

Here we've first created a new `Post` instance and a new `Tag` instance. Then, saved those instances to a new instance of our join model `PostTag`.

**Query**

To query many-to-many relationships, filter the join model based on one of the model's _id_.

```java
Amplify.DataStore.query(ContentTag.class, Where.matches(ContentTag.CONTENT.eq("YOUR_CONTENT_ID")),
    matches -> {
        while (matches.hasNext()) {
            ContentTag contentTag = matches.next();
            Log.i("Amplify DataStore", "Tag: " + contentTag.getTag());
        }
    }, failure -> {});
```

In this example, first filter the _join model_ `PostTag` with your `Post`'s _id, then map the `PostTag`s to `Tag`s.

**Delete**

Deleting the _join model instance_ will not delete any source model instances.

```java
Amplify.DataStore.delete(
    toBeDeletedPostTag,
    deleted -> Log.i("Amplify DataStore", "Deleted " + deleted),
    failure -> Log.e("Amplify DataStore", "Deletion failed", failure));
```
Both the `Post` and the `Tag` instances will not be deleted. Only the join model instances containing the link between a `Post` and a `Tag`.  

Deleting a _source model instance_ will also delete the join model instances containing the source model instance.
```java
Amplify.DataStore.delete(
    toBeDeletedTag,
    deleted -> Log.i("Amplify DataStore", "Deleted " + deleted),
    failure -> Log.e("Amplify DataStore", "Deletion failed", failure));

```
The `toBeDeletedTag` `Tag` instance and all `PostTag` instances where _tag_ is linked to `toBeDeletedTag` will be deleted.
