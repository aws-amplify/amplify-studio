:::NEW_COMMAND:::
:::CREATE:::
```swift
let item = :::MODEL:::(:::FIELDS:::)
Amplify.DataStore.save(item) { result in
    switch(result) {
    case .success(let savedItem):
        print("Saved item: \(savedItem.id)")
    case .failure(let error):
        print("Could not save item to DataStore: \(error)")
    }    
}
```
:::NEW_COMMAND:::
:::UPDATE:::
```swift
Amplify.DataStore.save(updatedItem) { result in
    switch(result) {
    case .success(let savedItem):
        print("Saved item: \(savedItem.id)")
    case .failure(let error):
        print("Could not save item to DataStore: \(error)")
    }    
}
```
:::NEW_COMMAND:::
:::DELETE:::
```swift
Amplify.DataStore.delete(toDeleteItem) { result in
    switch(result) {
    case .success:
        print("Deleted item: \(toDeleteItem.id)")
    case .failure(let error):
        print("Could not update data in Datastore: \(error)")
    }
}

```
:::NEW_COMMAND:::
:::QUERY:::
```swift
Amplify.DataStore.query(:::MODEL:::.self) { result in
    switch(result) {
    case .success(let items):
        for item in items {
            print(":::MODEL::: ID: \(item.id)")
        }
    case .failure(let error):
        print("Could not query DataStore: \(error)")
    }
}

```