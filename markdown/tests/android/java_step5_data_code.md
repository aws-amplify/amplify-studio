:::NEW_COMMAND:::
:::CREATE:::
```java
:::MODEL::: item = :::MODEL:::.builder()
    :::FIELDS:::
                .build();
Amplify.DataStore.save(item,
    success -> Log.i("DataStore", "Saved item: " + success.item().getId()),
    failure -> Log.e("DataStore", "Could not save item to DataStore", failure)
);
```
:::NEW_COMMAND:::
:::UPDATE:::
```java
Amplify.DataStore.save(updatedItem,
    success -> Log.i("DataStore", "Item updated: " + success.item().getId()),
    failure -> Log.e("DataStore", "Could not save item to DataStore", failure)
);
```
:::NEW_COMMAND:::
:::DELETE:::
```java
Amplify.DataStore.delete(toDeleteItem,
    success -> Log.i("DataStore", "Deleted item"),
    failure -> Log.e("DataStore", "Delete failed", failure)
);
```
:::NEW_COMMAND:::
:::QUERY:::
```java
Amplify.DataStore.query(
    :::MODEL:::.class,
    matchingItems -> {
        while (matchingItems.hasNext()) {
            :::MODEL::: item = matchingItems.next();
            Log.i("Amplify", "Id " + item.getId());
        }
    },
    failure -> Log.e("Amplify", "Could not query DataStore", failure)
);
```
