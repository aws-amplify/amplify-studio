Pull in the latest backend information into your app's code base. 

1. Open your Terminal, navigate to your Xcode workspace's directory, and run the following command:
```bash
:::AMPLIFY_PULL_COMMAND:::
```

2. Make sure to add the `AWSAPIPlugin()` and configure `Amplify`.
```swift
:::NO_COPY:::
let models = AmplifyModels()
```
```swift
let apiPlugin = AWSAPIPlugin(modelRegistration: models)
```
```swift
:::NO_COPY:::
let dataStorePlugin = AWSDataStorePlugin(modelRegistration: models)

do {
```
```swift
    try Amplify.add(plugin: apiPlugin)
```
```swift
:::NO_COPY:::
    try Amplify.add(plugin: dataStorePlugin)
    try Amplify.configure()
    print("Initialized Amplify");
} catch {
    print("Could not initialize Amplify: \(error)")
}
```