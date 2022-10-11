:::NEW_COMMAND:::
:::CREATE:::
```swift
do {
    let item = :::MODEL:::(:::FIELDS:::)
    let savedItem = try await Amplify.DataStore.save(item)
    print("Saved item: \(savedItem)")
} catch let error as DataStoreError {
    print("Error creating item: \(error)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
:::UPDATE:::
```swift
do {
    let updatedItem = try await Amplify.DataStore.save(item)
    print("Updated item: \(updatedItem)")
} catch let error as DataStoreError {
    print("Error updating item: \(error)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
:::DELETE:::
```swift
do {
    try await Amplify.DataStore.delete(itemToDelete)
    print("Deleted item: \(itemToDelete.identifier)")
} catch let error as DataStoreError {
    print("Error deleting item: \(error)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
:::QUERY:::
```swift
do {
    let items = try await Amplify.DataStore.query(:::MODEL:::.self)
    for item in items {
        print(":::MODEL::: ID: \(item.id)")
    }
} catch let error as DataStoreError {
    print("Error querying items: \(error)")
} catch {
    print("Unexpected error: \(error)")
}
```