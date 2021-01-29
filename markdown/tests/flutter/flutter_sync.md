Pull in the latest backend information into your app's code base.

1. Open your Terminal, navigate into your project’s root directory (where your pubspec.yaml is) and run:

```bash
:::AMPLIFY_PULL_COMMAND:::
```

2. Make sure to add the `AWSAPIPlugin()` and configure `Amplify`.

```dart
Amplify.addPlugin(AmplifyAPI());
```

```dart
:::NO_COPY:::
Amplify.addPlugin(AmplifyDataStore(modelProvider: ModelProvider.instance));

// Once Plugins are added, configure Amplify
await Amplify.configure(amplifyconfig);
try {
    setState(() {
    _amplifyConfigured = true;
    });
} catch (e) {
    print(e);
}
```
