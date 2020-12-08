:::NEW_COMMAND:::
:::ONE_TO_ONE:::

Example: **One post** (source model) has **one author** (target model).

**Create**

In order to save a 1:1 relationship, create the target model instance first and then save it to the source model instance.

```swift
let newAuthor = Author(name: "Rene Brandel")
let post = Post(content: "My first post!", author: newAuthor)

Amplify.DataStore.save(newAuthor)
    .flatMap { _ in Amplify.DataStore.save(post) }
    .sink { completion in
        if case .failure(let dataStoreError) = completion {
            print("An error occurred while saving: \(dataStoreError)")
        }
    } receiveValue: { value in
        print("Saved: \(value)")
    }
```
Here we've first created a new `Author` instance and then saved it to the `Post`'s "author" relationship field.

**Query**

To query one-to-one relationships, access the target model instance through its source model instance's field.

```swift
Amplify.DataStore.query(Post.self, byId: "YOUR_POST_ID")
    .sink{completion in
        if case .failure(let dataStoreError) = completion {
            print("An error occurred: \(dataStoreError)")
        }
    } receiveValue: { (post) in
        print("Posts: \(post)")
        print("Author: \(post?.author)")
    }
```

**Delete**

In one-to-one relationships, you'll need to manually remove both the source model instance and the target model instance. The deletion does not automatically cascade.

```swift
Amplify.DataStore.delete(post!)
    .append(Amplify.DataStore.delete(post!.author!))
    .sink { completion in
        if case let .failure(error) = completion {
            print("An error occurred in a preceding operation: \(error)")
        }
    } receiveValue: { _ in
        print("Everything is deleted")
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
Amplify.DataStore.save(publication)
    .flatMap { _ in
        Amplify.DataStore.save(
            Article(title: "Add auth to your app in 3 steps", publicationID: publication.id))
    }
    .sink {
        if case let .failure(error) = $0 {
            print("Error saving: \(error.localizedDescription)")
        }
    } receiveValue: { value in
        print("Successfully saved: \(value)")
    }
```
Here we've first created a new `Publication` instance and then saved its _id_ to the `Article`'s "publicationID" relationship field.

**Query**

To query one-to-many relationships, filter based on the source model instance's id on the target model.

```swift
let a = Article.keys
Amplify.DataStore.query(Article.self, where: a.publicationID == "YOUR_PUBLICATION_ID")
    .sink {
        if case let .failure(error) = $0 {
            print("Error querying: \(error)")
        }
    } receiveValue: { (articles) in
        print("Articles: \(articles)")
    }
```

**Delete**

In one-to-many relationships, if you delete the source model instance, you will also need to manually delete all related target model instances.

```swift
Amplify.DataStore.query(Article.self, where: Article.keys.publicationID == "YOUR_PUBLICATION_ID")
    .map { articles in
        articles.map { Amplify.DataStore.delete($0) }
    }
    .flatMap { Amplify.DataStore.delete(Publication.self, withId: "YOUR_PUBLICATION_ID") }
    .sink { completion in
        if case let .failure(error) = completion {
            print("An error occurred in a preceding operation: \(error)")
        }
    } receiveValue: {
        print($0)
        print("Everything completed successfully")
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

Amplify.DataStore.save(post)
    .flatMap { _ in Amplify.DataStore.save(tag) }
    .flatMap { _ in Amplify.DataStore.save(PostTag(post: post, tag: tag)) }
    .sink {
        if case let .failure(error) = $0 {
            print("Error saving: \(error.localizedDescription)")
        }
    } receiveValue: {
        print("Saved PostTag: \($0)")
    }
```

Here we've first created a new `Post` instance and a new `Tag` instance. Then, saved those instances to a new instance of our join model `PostTag`.

**Query**

To query many-to-many relationships, filter the join model based on one of the model's _id_.

```swift
let pt = PostTag.keys
Amplify.DataStore.query(PostTag.self, where: field("postID").eq("YOUR_POST_ID"))
    .sink {
        if case let .failure(error) = $0 {
            print(error)
        }
    } receiveValue: { (postTags) in
        print("Tags: \(postTags.map { $0.tag })")
    }
```

In this example, first filter the _join model_ `PostTag` with your `Post`'s _id, then map the `PostTag`s to `Tag`s.

**Delete**

Deleting the _join model instance_ will not delete any source model instances.

```swift
Amplify.DataStore.delete(toBeDeletedPostTag)
    .sink { completion in
        if case .failure(let dataStoreError) = completion {
            print("An error occurred while deleting: \(dataStoreError)")
        }
    } receiveValue: { value in
        print("PostTag deleted")
    }
```
Both the `Post` and the `Tag` instances will not be deleted. Only the join model instances containing the link between a `Post` and a `Tag`.  

Deleting a _source model instance_ will also delete the join model instances containing the source model instance.
```swift
Amplify.DataStore.delete(toBeDeletedTag)
    .sink { completion in
        if case .failure(let dataStoreError) = completion {
            print("An error occurred while deleting: \(dataStoreError)")
        }
    } receiveValue: { value in
        print("Tag and all their PostTag deleted")
    }
```
The `toBeDeletedTag` `Tag` instance and all `PostTag` instances where _tag_ is linked to `toBeDeletedTag` will be deleted.