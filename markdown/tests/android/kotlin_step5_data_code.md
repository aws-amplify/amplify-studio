:::NEW_COMMAND:::
:::CREATE:::
```kt
val item: :::MODEL::: = :::MODEL:::.builder()
    :::FIELDS:::
                .build()
Amplify.DataStore.save(
        item,
        { success -> Log.i("Amplify", "Saved item: " + success.item().name) },
        { error -> Log.e("Amplify", "Could not save item to DataStore", error) }
)
```
:::NEW_COMMAND:::
:::UPDATE:::
```kt
Amplify.DataStore.save(
        updatedItem,
        { success -> Log.i("Amplify", "Updated item: " + success.item().name) },
        { error -> Log.e("Amplify", "Could not save item to DataStore", error) }
)
```
:::NEW_COMMAND:::
:::DELETE:::
```kt
Amplify.DataStore.delete(toDeleteItem,
    { deleted -> Log.i("Amplify", "Deleted item.") },
    { failure -> Log.e("Amplify", "Delete failed.", failure) }
)
```
:::NEW_COMMAND:::
:::QUERY:::
```kt
Amplify.DataStore.query(
     :::MODEL:::::class.java,
     { items ->
         while (items.hasNext()) {
             val item = items.next()
             Log.i("Amplify", "Queried item: " + item.id)
         }
     },
     { failure -> Log.e("Tutorial", "Could not query DataStore", failure) }
)
```