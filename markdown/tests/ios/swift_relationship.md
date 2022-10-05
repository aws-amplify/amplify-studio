:::NEW_COMMAND:::
:::ONE_TO_ONE:::

Example: **One post** (source model) has **one author** (target model).

**Create**

In order to save a 1:1 relationship, create the target model instance first and then save it to the source model instance.

```swift
let newAuthor = Author(name: "Rene Brandel")
let post = Post(content: "My first post!", author: newAuthor)

do {
    let savedAuthor = try await Amplify.DataStore.save(newAuthor)
    let savedPost = try await Amplify.DataStore.save(post)
    print("Saved Author: \(savedAuthor) | Saved Post: \(savedPost)")
} catch let error as DataStoreError {
    print("An error occurred: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```
Here we've first created a new `Author` instance and then saved it to the `Post`'s "author" relationship field.

**Query**

To query one-to-one relationships, access the target model instance through its source model instance's field.

```swift
do { 
    let post = try await Amplify.DataStore.query(Post.self, byId: "YOUR_POST_ID")
    print("Posts: \(post)")
    print("Author: \(post?.author)")
} catch let error as DataStoreError {
    print("An error occurred: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```

**Delete**

In one-to-one relationships, you'll need to manually remove both the source model instance and the target model instance. The deletion does not automatically cascade.

```swift
do { 
    try await Amplify.DataStore.delete(post.author)
    try await Amplify.DataStore.delete(post)
    print("Everything is deleted")
} catch let error as DataStoreError {
    print("An error occurred in a preceding operation: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```

In this example, the `Post`'s "author" field will be cleared and the `Author` model instance will be deleted.

:::NEW_COMMAND:::
:::ONE_TO_MANY:::

Example: **One publication** (source model) has **many articles** (target model)

**Create**

In order to save a one-to-many relationship, create the source model instance first and then save its _id_ to the target model instance's relationship source field.

```swift
let publication = Publication(name: "Amplify Weekly")
do { 
    let savedPublication = try await Amplify.DataStore.save(publication)
    let savedArticle = try await Amplify.DataStore.save(
        Article(title: "Add auth to your app in 3 steps", publicationID: publication.id))
    )
    print("Successfully saved: \(savedPublication), \(savedArticle)")
} catch let error as DataStoreError {
    print("Error saving: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```
Here we've first created a new `Publication` instance and then saved its _id_ to the `Article`'s "publicationID" relationship field.

**Query**

To query one-to-many relationships, filter based on the source model instance's id on the target model.

```swift
let a = Article.keys
do { 
    let articles = try await Amplify.DataStore.query(
        Article.self, where: a.publicationID == "YOUR_PUBLICATION_ID"
    )
    print("Articles: \(articles)")
} catch let error as DataStoreError { 
    print("Error querying: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```

**Delete**

In one-to-many relationships, if you delete the source model instance, you will also need to manually delete all related target model instances.

```swift
do { 
    let articles = try await Amplify.DataStore.query(
        Article.self, 
        where: Article.keys.publicationID == "YOUR_PUBLICATION_ID"
    )
    for article in articles { 
        Amplify.DataStore.delete(article) 
    }
    try await Amplify.DataStore.delete(Publication.self, withId: "YOUR_PUBLICATION_ID")
    print("Everything completed successfully")
} catch let error as DataStoreError { 
    print("An error occurred in a preceding operation: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```

In this example, the `Publication` "toBeDeletedPublication" and all of its related `Article` model instances will be deleted.

:::NEW_COMMAND:::
:::MANY_TO_MANY:::

Example: **Posts** have **many tags** and **Tags** have **many posts**. 

In any many-to-many relationship, Amplify admin UI automatically creates a "join model" consisting of the combination of the source model names. In our example, Amplify automatically creates a **PostTag** join model.

**Create**

In order to save a many-to-many relationship, create both model instance first and then save them to a new join model instance.

```swift
let post = Post(body: "How to build deploy a web app on AWS Amplify")
let tag = Tag(label: "static-web-hosting")

do { 
    let savedPost = try await Amplify.DataStore.save(post)
    let savedTag = try await Amplify.DataStore.save(tag)
    let savedPostTag = try await Amplify.DataStore.save(PostTag(post: post, tag: tag))
    print("Saved PostTag: \(savedPostTag)")
} catch let error as DataStoreError { 
    print("Error saving: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```

Here we've first created a new `Post` instance and a new `Tag` instance. Then, saved those instances to a new instance of our join model `PostTag`.

**Query**

To query many-to-many relationships, filter the join model based on one of the model's _id_.

```swift
let pt = PostTag.keys
do { 
    let postTags = try await Amplify.DataStore.query(
        PostTag.self,
        where: field("postID").eq("YOUR_POST_ID")
    )
    print("Tags: \(postTags.map(\.tag))")
} catch let error as DataStoreError { 
    print("Error querying: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```

In this example, first filter the _join model_ `PostTag` with your `Post`'s _id, then map the `PostTag`s to `Tag`s.

**Delete**

Deleting the _join model instance_ will not delete any source model instances.

```swift
do { 
    try await Amplify.DataStore.delete(toBeDeletedPostTag)
    print("PostTag deleted")
} catch let error as DataStoreError { 
    print("An error occurred while deleting: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```
Both the `Post` and the `Tag` instances will not be deleted. Only the join model instances containing the link between a `Post` and a `Tag`.  

Deleting a _source model instance_ will also delete the join model instances containing the source model instance.
```swift
do { 
    try await Amplify.DataStore.delete(toBeDeletedTag)
    print("Tag and all their PostTag deleted")
} catch let error as DataStoreError { 
    print("An error occurred while deleting: \(error)")
} catch { 
    print("Unexpected error: \(error)")
}
```
The `toBeDeletedTag` `Tag` instance and all `PostTag` instances where _tag_ is linked to `toBeDeletedTag` will be deleted.