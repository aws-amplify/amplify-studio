Amplify for Flutter is distributed via pub.dev.

1. Add the dependencies to **pubspec.yaml**:
```yaml
:::NO_COPY:::
dependencies:
  flutter:
    sdk: flutter
```
```yaml
  amplify_flutter: "<1.0.0"
  # amplify_api: "<1.0.0" // UNCOMMENT this line once backend is deployed
  amplify_datastore: "<1.0.0"
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

If you are using Flutter v2 and encountering build errors involving minimum deployment targets, you may need to update your app's `Podfile` in the `ios` directory.
You should update the post_install hook to include the following:

```ruby
:::NO_COPY:::
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
```
```ruby
    target.build_configurations.each do |config|
      config.build_settings.delete 'IPHONEOS_DEPLOYMENT_TARGET'
    end
```
```ruby
:::NO_COPY:::
   end
 end
 ```

4. (Android only) Open **android/app/build.gradle** and update the *minSdkVersion*:
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
        targetSdkVersion 29
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
    }
    ...
}
```

5. Go to **main.dart** and add the following lines to initialize the Amplify Libraries:
```dart
// Amplify Flutter Packages
import 'package:amplify_flutter/amplify.dart';
// import 'package:amplify_api/amplify_api.dart'; // UNCOMMENT this line once backend is deployed
import 'package:amplify_datastore/amplify_datastore.dart';

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
