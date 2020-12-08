Amplify dependencies are installed through CocoaPods. Open a terminal window and navigate to the location of the Xcode project for your app.

1. Initialize CocoaPods:
```bash
pod init
```

2. Update the **Podfile** to include the following pods:
```ruby
:::NO_COPY:::
target '<YOUR_APP_NAME>' do
    use_frameworks!

    # Pods for <YOUR_APP_NAME>
```
```ruby
    pod 'Amplify'
    pod 'AmplifyPlugins/AWSAPIPlugin'
    pod 'AmplifyPlugins/AWSDataStorePlugin'
```
```ruby
:::NO_COPY:::
    target '<YOUR_APP_NAME>Tests' do
        ...
    end
end
```

3. Install the Amplify pod into your project:
```bash
pod install --repo-update
```

4. **Close** your existing Xcode window

5. Open the new Xcode workspace file
```
xed .
```

6. Go to **<YOUR_APP_NAME>App.swift** and add the following lines to initialize Amplify libraries:
```swift
import Amplify
import AmplifyPlugins
```

```swift
:::NO_COPY:::
@main
struct <YOUR_APP_NAME>App: App {
```
```swift
    public init() {
        let dataStorePlugin = AWSDataStorePlugin(modelRegistration: AmplifyModels())
        //let apiPlugin = AWSAPIPlugin(modelRegistration: AmplifyModels()) // UNCOMMENT this line once backend is deployed

        do {
            try Amplify.add(plugin: dataStorePlugin)
            //try Amplify.add(plugin: apiPlugin) // UNCOMMENT this line once backend is deployed
            try Amplify.configure()
            print("Initialized Amplify");
        } catch {
            print("Could not initialize Amplify: \(error)")
        }
    }
```
```swift
:::NO_COPY:::
}
```
