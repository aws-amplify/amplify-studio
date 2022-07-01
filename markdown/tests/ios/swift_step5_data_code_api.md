:::NEW_COMMAND:::
:::CREATE:::

```js
import Amplify
import AWSPluginsCore
```

```js
:::NO_COPY:::
...
```

```js
func update:::MODEL:::() {
    // Retrieve your :::MODEL::: using Amplify.API.query
    var model = :::MODEL:::(name: "my first :::MODEL:::", description: ":::MODEL::: description")
    model.description = "updated description"
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
}
```

:::NEW_COMMAND:::
:::UPDATE:::

```js
import Amplify
import AWSPluginsCore
```

```js
:::NO_COPY:::
...
```

```js
func update:::MODEL:::() {
    // Retrieve your :::MODEL::: using Amplify.API.query
    var model = :::MODEL:::(name: "my first :::MODEL:::", description: ":::MODEL::: description")
    model.description = "updated description"
    Amplify.API.mutate(request: .update(model)) { event in
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
}
```

:::NEW_COMMAND:::
:::DELETE:::

```js
import Amplify
import AWSPluginsCore
```

```js
:::NO_COPY:::
...
```

```js
func update:::MODEL:::() {
    // Retrieve your :::MODEL::: using Amplify.API.query
    var model = :::MODEL:::(name: "my first :::MODEL:::", description: ":::MODEL::: description")
    model.description = "updated description"
    Amplify.API.mutate(request: .delete(model)) { event in
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
}
```

:::NEW_COMMAND:::
:::QUERY:::

```js
import Amplify
import AWSPluginsCore
```

```js
:::NO_COPY:::
...
```

```js
func get:::MODEL:::() {
    Amplify.API.query(request: .get(:::MODEL:::.self, byId: "ENTER MODEL ID HERE")) { event in
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
