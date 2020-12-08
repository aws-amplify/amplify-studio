:::NEW_COMMAND:::
:::ONE_TO_ONE:::

Example: **One post** (source model) has **one author** (target model).

**Create**

In order to save a 1:1 relationship, create the target model instance first and then save it to the source model instance.

```js
const newAuthor = await DataStore.save(new Author({
  name: "Rene Brandel"
}))

const post = await DataStore.save(
  new Post({
    title: "My first post!",
    content: "Lorem ipsum ",
    author: newAuthor
  })
);
```
Here we've first created a new `Author` instance and then saved it to the `Post`'s "author" relationship field.

**Query**

To query one-to-one relationships, access the target model instance through its source model instance's field.

```js
const post = await DataStore.query(Post, "YOUR_POST_ID")
const author = post.author
```

**Delete**

In one-to-one relationships, if the target model instance is deleted, it will also clear the source model instance's relationship field.

```js
const post = await DataStore.query(Post, "YOUR_POST_ID")
await DataStore.delete(post.author)
```

In this example, the `Post`'s "author" field will be cleared and the `Author` model instance will be deleted.

:::NEW_COMMAND:::
:::ONE_TO_MANY:::

Example: **One publication** (source model) has **many articles** (target model)

**Create**

In order to save a one-to-many relationship, create the source model instance first and then save its _id_ to the target model instance's relationship source field.

```js
const publication = await DataStore.save(new Publication({
  name: "Amplify Weekly"
}))

const article = await DataStore.save(new Article({
  title: "Add auth to your app in 3 steps",
  publicationID: publication.id
}))
```
Here we've first created a new `Publication` instance and then saved its _id_ to the `Article`'s "publicationID" relationship field.

**Query**

To query one-to-many relationships, filter based on the source model instance's id on the target model.

```js
const articles = (await DataStore.query(Article))                    
                    .filter(a => a.publicationID === "YOUR_PUBLICATION_ID");
```

**Delete**

In one-to-many relationships, if you delete the source model instance, it will also delete all related target model instances.

```js
await DataStore.delete(toBeDeletedPublication)
```

In this example, the `Publication` "toBeDeletedPublication" and all of its related `Article` model instances will be deleted.

:::NEW_COMMAND:::
:::MANY_TO_MANY:::

Example: **Posts** have **many tags** and **Tags** have **many posts**. 

In any many-to-many relationship, Amplify admin UI automatically creates a "join model" consisting of the combination of the source model names. In our example, Amplify automatically creates a **PostTag** join model.

**Create**

In order to save a many-to-many relationship, create both model instance first and then save them to a new join model instance.

```js
const post = await DataStore.save(new Post({
  body: "How to build deploy a web app on AWS Amplify"
}))

const tag = await DataStore.save(new Tag({
  label: "static-web-hosting"
}))

const postTag = await DataStore.save(new PostTag({
  post: post,
  tag: tag
}))
```

Here we've first created a new `Post` instance and a new `Tag` instance. Then, saved those instances to a new instance of our join model `PostTag`.

**Query**

To query many-to-many relationships, filter the join model based on one of the model's _id_.

```js
const tags = (await DataStore.query(PostTag))                
                .filter(pt => pt.post.id === "YOUR_POST_ID")
                .map(pt => pt.tag)
```

In this example, first filter the _join model_ `PostTag` with your `Post`'s _id, then map the `PostTag`s to `Tag`s.

**Delete**

Deleting the _join model instance_ will not delete any source model instances.

```js
await DataStore.delete(toBeDeletedPostTag)
```
Both the `Post` and the `Tag` instances will not be deleted. Only the join model instances containing the link between a `Post` and a `Tag`.  

Deleting a _source model instance_ will also delete the join model instances containing the source model instance.
```js
await DataStore.delete(toBeDeletedTag)
```
The `toBeDeletedTag` `Tag` instance and all `PostTag` instances where _tag_ is linked to `toBeDeletedTag` will be deleted.