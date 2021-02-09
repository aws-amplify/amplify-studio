Amplify for Flutter is distributed via pub.dev.

1. Add the dependencies to `pubspec.yaml`:
```yaml
:::NO_COPY:::
dependencies:
  flutter:
    sdk: flutter
```
```yaml
  amplify_flutter: "<1.0.0"
  amplify_api: "<1.0.0"
  amplify_datastore: "<1.0.0"
```

2. Click **Pub Get** in the "Flutter commands" bar to install Amplify Libraries

3. Open **ios/Podfile** and update the platform target:
```ruby
:::NO_COPY:::
# Uncomment this line to define a global platform for your project
```
```ruby
platform :ios, '13.0'
```

4. Go to **main.dart** and add the following lines to initialize the Amplify Libraries:
```dart
// Amplify Flutter Packages
import 'package:amplify_flutter/amplify.dart';
import 'package:amplify_api/amplify_api.dart';
import 'package:amplify_datastore/amplify_datastore.dart';
import 'package:amplify_datastore_plugin_interface/amplify_datastore_plugin_interface.dart';

// Generated in previous step
import 'models/ModelProvider.dart';
import 'amplifyconfiguration.dart';
```
```dart
:::NO_COPY:::
//...
class _MyHomePageState extends State<MyHomePage> {
```
```dart
  bool _amplifyConfigured = false;
```
```dart
:::NO_COPY:::
  @override
  initState() {
```
```dart
    super.initState();
    _configureAmplify();
```
```dart
:::NO_COPY:::
  }
```
```dart
  void _configureAmplify() async {

    // Amplify.addPlugin(AmplifyAPI()); // UNCOMMENT this line once backend is deployed
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
  }
```
```dart
:::NO_COPY:::
}
```
