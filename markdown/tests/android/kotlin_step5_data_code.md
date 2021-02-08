:::NEW_COMMAND:::
:::CREATE:::
```kotlin
val item = :::MODEL:::.builder()
    :::FIELDS:::
    .build()
Amplify.DataStore.save(item,
    { Log.i("DataStore", "Saved item: ${it.item().name}") },
    { Log.e("DataStore", "Could not save item to DataStore", it) }
)
```
:::NEW_COMMAND:::
:::UPDATE:::
```kotlin
Amplify.DataStore.save(updatedItem,
    { Log.i("DataStore", "Updated item: ${it.item().name}") },
    { Log.e("DataStore", "Could not save item to DataStore", it) }
)
```
:::NEW_COMMAND:::
:::DELETE:::
```kotlin
Amplify.DataStore.delete(toDeleteItem,
    { Log.i("DataStore", "Deleted item") },
    { Log.e("DataStore", "Delete failed", it) }
)
```
:::NEW_COMMAND:::
:::QUERY:::
```kotlin
Amplify.DataStore.query(:::MODEL:::::class.java,
    { matchingItems ->
        while (matchingItems.hasNext()) {
            Log.i("Amplify", "Queried item: ${matchingItems.next().id}")
        }
    },
    { Log.e("DataStore", "Could not query DataStore", it) }
)
```
