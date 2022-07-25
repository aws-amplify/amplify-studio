:::NEW_COMMAND:::
:::CREATE:::

```swift
var model = :::MODEL:::(:::FIELDS:::)
Amplify.API.mutate(request: .create(model)) { event in
    switch event {
    case .success(let result):
        switch result {
        case .success(let model):
            print("Successfully created :::MODEL:::: \(model)")
        case .failure(let error):
            print("Got failed result with \(error.errorDescription)")
        }
    case .failure(let error):
        print("Got failed event with error \(error)")
    }
}
```

:::NEW_COMMAND:::
:::UPDATE:::

```swift
// Retrieve your :::MODEL::: using Amplify.API.query
Amplify.API.mutate(request: .update(updatedModel)) { event in
    switch event {
    case .success(let result):
        switch result {
        case .success(let model):
            print("Successfully updated :::MODEL:::: \(model)")
        case .failure(let error):
            print("Got failed result with \(error.errorDescription)")
        }
    case .failure(let error):
        print("Got failed event with error \(error)")
    }
}
```

:::NEW_COMMAND:::
:::DELETE:::

```swift
// Retrieve your :::MODEL::: using Amplify.API.query
Amplify.API.mutate(request: .delete(modelToBeDeleted)) { event in
    switch event {
    case .success(let result):
        switch result {
        case .success(let model):
            print("Successfully deleted :::MODEL:::: \(model)")
        case .failure(let error):
            print("Got failed result with \(error.errorDescription)")
        }
    case .failure(let error):
        print("Got failed event with error \(error)")
    }
}
```

:::NEW_COMMAND:::
:::QUERY:::

```swift
func get:::MODEL:::() {
    Amplify.API.query(request: .get(:::MODEL:::.self, byId: "YOUR_RECORD_ID")) { event in
        switch event {
        case .success(let result):
            switch result {
            case .success(let model):
                guard let model = model else {
                    print("Could not find :::MODEL:::")
                    return
                }
                print("Successfully retrieved :::MODEL:::: \(model)")
            case .failure(let error):
                print("Got failed result with \(error.errorDescription)")
            }
        case .failure(let error):
            print("Got failed event with error \(error)")
        }
    }
}
```
