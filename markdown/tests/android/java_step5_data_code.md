:::NEW_COMMAND:::
:::CREATE:::
```java
:::MODEL::: item = :::MODEL:::.builder()
    :::FIELDS:::
                .build();
Amplify.DataStore.save(
    item,
    success -> Log.i("Amplify", "Saved item: " + success.item().getId()),
    error -> Log.e("Amplify", "Could not save item to DataStore", error)
);
```
:::NEW_COMMAND:::
:::UPDATE:::
```java
Amplify.DataStore.save(
    updatedItem,
    success -> Log.i("Amplify", "Item updated: " + success.item().getId()),
    error -> Log.e("Amplify", "Could not save item to DataStore", error)
);
```
:::NEW_COMMAND:::
:::DELETE:::
```java
Amplify.DataStore.delete(toDeleteItem,
    deleted -> Log.i("Amplify", "Deleted item."),
    failure -> Log.e("Amplify", "Delete failed.", failure)
);
```
:::NEW_COMMAND:::
:::QUERY:::
```java
Amplify.DataStore.query(
       :::MODEL:::.class,
       items -> {
           while (items.hasNext()) {
               :::MODEL::: item = items.next();
               Log.i("Amplify", "Id " + item.getId());
           }
       },
       failure -> Log.e("Amplify", "Could not query DataStore", failure)
);

```