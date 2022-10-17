:::NEW_COMMAND:::
:::CREATE:::

```swift
import Amplify
import AWSPluginsCore
```

```swift
:::NO_COPY:::
...
```

```swift
func update:::MODEL:::() async {
    // Retrieve your :::MODEL::: using Amplify.API.query
    var model = :::MODEL:::(name: "my first :::MODEL:::", description: ":::MODEL::: description")
    model.description = "updated description"
    do {
        let result = try await Amplify.API.mutate(request: .create(model))
        switch result {
        case .success(let model):
            print("Successfully created :::MODEL:::: \(model)")
        case .failure(let graphQLError):
            print("Failed to create graphql \(graphQLError)")
        }
    } catch let error as APIError {
        print("Failed to create :::MODEL::: - \(error)")
    } catch {
        print("Unexpected error: \(error)")
    }
}
```

:::NEW_COMMAND:::
:::UPDATE:::

```swift
import Amplify
import AWSPluginsCore
```

```swift
:::NO_COPY:::
...
```

```swift
func update:::MODEL:::() async {
    // Retrieve your :::MODEL::: using Amplify.API.query
    var model = :::MODEL:::(name: "my first :::MODEL:::", description: ":::MODEL::: description")
    model.description = "updated description"
    do {
        let result = try await Amplify.API.mutate(request: .update(model))
        switch result {
        case .success(let model):
            print("Successfully updated :::MODEL:::: \(model)")
        case .failure(let error):
            print("Got failed result with \(error.errorDescription)")
        }
    } catch let error as APIError {
        print("Failed to update :::MODEL::: - \(error)")
    } catch {
        print("Unexpected error: \(error)")
    }
}
```

:::NEW_COMMAND:::
:::DELETE:::

```swift
import Amplify
import AWSPluginsCore
```

```swift
:::NO_COPY:::
...
```

```swift
func update:::MODEL:::() async {
    // Retrieve your :::MODEL::: using Amplify.API.query
    var model = :::MODEL:::(name: "my first :::MODEL:::", description: ":::MODEL::: description")
    model.description = "updated description"
    do {
        let result = try await Amplify.API.mutate(request: .delete(model))
        switch result {
        case .success(let model):
            print("Successfully deleted :::MODEL:::: \(model)")
        case .failure(let error):
            print("Got failed result with \(error.errorDescription)")
        }
    } catch let error as APIError {
        print("Failed to delete :::MODEL::: - \(error)")
    } catch {
        print("Unexpected error: \(error)")
    }
}
```

:::NEW_COMMAND:::
:::QUERY:::

```swift
import Amplify
import AWSPluginsCore
```

```swift
:::NO_COPY:::
...
```

```swift
func get:::MODEL:::() async {
    do {
        let result = try await Amplify.API.query(
            request: .get(:::MODEL:::.self,
            byId: "ENTER MODEL ID HERE")
        )
        switch result {
        case .success(let model):
            guard let model = model else {
                print("Could not find model")
                return
            }
            print("Successfully retrieved model: \(model)")
        case .failure(let error):
            print("Got failed result with \(error)")
        }
    } catch let error as APIError {
        print("Failed to query :::MODEL::: - \(error)")
    } catch {
        print("Unexpected error: \(error)")
    }
}
```
