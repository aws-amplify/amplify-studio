:::NEW_COMMAND:::
:::ONE_TO_ONE:::

Example: **One post** (source model) has **one author** (target model).

**Create**

In order to save a 1:1 relationship, create the target model instance first and then save it to the source model instance.

```dart
Author newAuthor = Author(name: "Rene Brandel");
Post post = Post(content: "My first post!", author: newAuthor);

try {
    await Amplify.DataStore.save(newAuthor);
    print("Author saved");
    await Amplify.DataStore.save(post);
    print("Post saved");
} catch (e) {
    print("An error occured while saving: $e");
}
```

Here we've first created a new `Author` instance and then saved it to the `Post`'s "author" relationship field.

**Query**

To query one-to-one relationships, access the target model instance through its source model instance's field.

```dart
try {
    List<Posts> posts = await Amplify.DataStore.query(Post.classType, where: Post.ID.eq("YOUR_POST_ID"));
    if (posts.isNotEmpty) {
        print("Post: ${posts.first}");
        print("Author: ${posts.first.author}");
    } else {
        print("No posts found");
    }
    
} catch (e) {
    print("An error occurred: $e");
}
```

**Delete**

In one-to-one relationships, if the target model instance is deleted, it will also clear the source model instance's relationship field.

```dart
try {
    await Amplify.DataStore.delete(post.author);
    print('Author deleted');

} catch (e) {
    print('An error occurred in the preceding operation: $e');
}
```

In this example, the `Post`'s "author" field will be cleared and the `Author` model instance will be deleted.

:::NEW_COMMAND:::
:::ONE_TO_MANY:::

Example: **One publication** (source model) has **many articles** (target model)

**Create**

In order to save a one-to-many relationship, create the source model instance first and then save its _id_ to the target model instance's relationship source field.

```dart
Publication publication = Publication(name: "Amplify Weekly");
Article article = Article(
    title: "Add auth to your app in 3 steps", 
    publicationID: publication.id);

try {
    await Amplify.DataStore.save(publication);
    await Amplify.DataStore.save(article);
    print("Successfully saved: $article");

} catch (e) {
    print("Error saving: $e");
}
```

Here we've first created a new `Publication` instance and then saved its _id_ to the `Article`'s "publicationID" relationship field.

**Query**

To query one-to-many relationships, filter based on the source model instance's id on the target model.

```dart
try {
    List<Article> articles = await Amplify.DataStore.query(
        Article.classType,
        where: Article.PUBLICATION_ID.eq("YOUR_PUBLICATION_ID")
    );
    print("Articles: $articles");

} catch (e) {
    print("Error querying: $e");
}
```

**Delete**

In one-to-many relationships, if you delete the source model instance, you will also need to manually delete all related target model instances.

```dart
try {
    (await Amplify.DataStore.query(
        Article.classType,
        where: Article.PUBLICATION_ID.eq("YOUR_PUBLICATION_ID")
    )).forEach((article) async {
        await Amplify.DataStore.delete(article);
    });

    (await Amplify.DataStore.query(
        Publication.classType,
        where: Publication.ID.eq("YOUR_PUBLICATION_ID")
    )).forEach((publication) async {
        await Amplify.DataStore.delete(publication);
    });
    
    print("Everything completed successfully");

} catch (e) {
    print('An error occurred in the preceding operation: $e');
}
```

In this example, the `Publication` "toBeDeletedPublication" and all of its related `Article` model instances will be deleted.

:::NEW_COMMAND:::
:::MANY_TO_MANY:::

Example: **Posts** have **many tags** and **Tags** have **many posts**. 

In any many-to-many relationship, Amplify admin UI automatically creates a "join model" consisting of the combination of the source model names. In our example, Amplify automatically creates a **PostTag** join model.

**Create**

In order to save a many-to-many relationship, create both model instance first and then save them to a new join model instance.

```dart
Post post = Post(body: "How to build deploy a web app on AWS Amplify");
Tag tag = Tag(label: "static-web-hosting");
PostTag postTag = PostTag(post: post, tag: tag);

try {
    await Amplify.DataStore.save(post);
    await Amplify.DataStore.save(tag);
    await Amplify.DataStore.save(postTag);
    print("Saved PostTag: $postTag");

} catch (e) {
    print("Error saving: $e");
}
```

Here we've first created a new `Post` instance and a new `Tag` instance. Then, saved those instances to a new instance of our join model `PostTag`.

**Query**

To query many-to-many relationships, filter the join model based on one of the model's _id_.

```dart
try {
    List<Tag> tags = (await Amplify.DataStore.query(
        PostTag.classType, 
        where: PostTag.POST.eq("YOUR_POST_ID")
    )).map((postTag) => postTag.tag).toList();

    print("Tags: $tags");

} catch (e) {
    print("Error querying: $e");
}
```

In this example, first filter the _join model_ `PostTag` with your `Post`'s _id, then map the `PostTag`s to `Tag`s.

**Delete**

Deleting the _join model instance_ will not delete any source model instances.

```dart
try {
    await Amplify.DataStore.delete(toBeDeletedPostTag);
    print("PostTag deleted");

} catch (e) {
    print("An error occurred while deleting: $e");
}
```
Both the `Post` and the `Tag` instances will not be deleted. Only the join model instances containing the link between a `Post` and a `Tag`.  

Deleting a _source model instance_ will also delete the join model instances containing the source model instance.
```dart
try {
    await Amplify.DataStore.delete(toBeDeletedTag);
    print("Tag and all their PostTag deleted");

} catch (e) {
    print("An error occurred while deleting: $e");
}
```
The `toBeDeletedTag` `Tag` instance and all `PostTag` instances where _tag_ is linked to `toBeDeletedTag` will be deleted.