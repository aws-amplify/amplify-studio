:::NEW_COMMAND:::
:::ONE_TO_ONE:::

Example: **One post** (source model) has **one author** (target model).

**Create**

In order to save a 1:1 relationship, create the target model instance first and then save it to the source model instance.

```dart
Author newAuthor = Author(name: "Rene Brandel")
Post post = Post(content: "My first post!", author: newAuthor)

await Amplify.DataStore.save(newAuthor);
print("Author saved");
await Amplify.DataStore.save(post);
print("Post saved");
```

Here we've first created a new `Author` instance and then saved it to the `Post`'s "author" relationship field.

**Query**

To query one-to-one relationships, access the target model instance through its source model instance's field.

```dart
List<Posts> posts = await Amplify.DataStore.query(Post.classType, where: Post.ID.eq("YOUR_POST_ID"));
print("Post: " + posts[0]);
print("Author: " + posts[0]?.author);
```

**Delete**

In one-to-one relationships, if the target model instance is deleted, it will also clear the source model instance's relationship field.

```dart
await Amplify.DataStore.delete(newAuthor);
```

In this example, the `Post`'s "author" field will be cleared and the `Author` model instance will be deleted.

:::NEW_COMMAND:::
:::ONE_TO_MANY:::

Example: **One publication** (source model) has **many articles** (target model)

**Create**

TBD

**Query**

TBD

**Delete**

TBD

**Create**

TBD

**Query**

TBD

**Delete**

TBD
