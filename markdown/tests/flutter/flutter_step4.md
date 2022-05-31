Amplify for Flutter is distributed via pub.dev.

1. Add the dependencies to **pubspec.yaml**:

```yaml
:::NO_COPY:::
dependencies:
  flutter:
    sdk: flutter
```

```yaml
amplify_flutter: ^0.5.0
amplify_datastore: ^0.5.0
# amplify_api: ^0.5.0 // UNCOMMENT this line after backend is deployed
```

2. Click **Pub Get** in the "Flutter commands" bar to install Amplify Libraries

3. (iOS only) Open **ios/Podfile** and update the platform target:

```ruby
:::NO_COPY:::
# Uncomment this line to define a global platform for your project
```

```ruby
platform :ios, '13.0'
```

4. (Android only) Open **android/app/build.gradle** and update the _minSdkVersion_:

```gradle
:::NO_COPY:::
android {
    ....
    defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.example.flutter_app"

```

```gradle
        minSdkVersion 21
```

```gradle
:::NO_COPY:::
        targetSdkVersion 30
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
    }
    ...
}
```

5. Go to **main.dart** and add the following lines to initialize the Amplify Libraries:

```dart
// Amplify Flutter Packages
import 'package:amplify_flutter/amplify_flutter.dart';
import 'package:amplify_datastore/amplify_datastore.dart';
// import 'package:amplify_api/amplify_api.dart'; // UNCOMMENT this line after backend is deployed

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

    // await Amplify.addPlugin(AmplifyAPI()); // UNCOMMENT this line after backend is deployed
    await Amplify.addPlugin(AmplifyDataStore(modelProvider: ModelProvider.instance));

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
