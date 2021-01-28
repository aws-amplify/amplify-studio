Amplify for Flutter is distributed via pub.dev.

1. Open your **app**'s `pubspec.yaml` and add the following 3 dependencies below the line "sdk:flutter".

```yaml
dependencies:
  flutter:
    sdk: flutter

  amplify_flutter: "<1.0.0"
  amplify_api: "<1.0.0"
  amplify_datastore: "<1.0.0"
```

2. Run **Flutter Pub Get**

Android Studio requires you to sync your project with your new configuration. To do this, you can click **Flutter** in the notification bar above the file editor.

Alternatively, you can open a terminal window, cd into your project's root directory (where your pubspec.yaml is) and run:

```bash
flutter pub get
```

When complete, you will see _Process finished with exit code 0_ in the output of the _Messages_ tab at the bottom of your screen.

3. Before using any methods in the Amplify Flutter Library, it's important to add all necessary plugins and to call configure once in your app. The steps below will guide you through configuring Amplify Flutter at the root level of your flutter app.

Import the necessary dart dependencies at the top of main.dart:

```dart
// Amplify Flutter Packages
import 'package:amplify_flutter/amplify.dart';
import 'package:amplify_datastore/amplify_datastore.dart';
import 'package:amplify_datastore_plugin_interface/amplify_datastore_plugin_interface.dart';

// Generated in previous step
import 'codegen/ModelProvider.dart';
import 'amplifyconfiguration.dart';
```

Add the following code to your application's root Stateful Widget, for a blank Flutter app this should be the `class _MyHomePageState extends State<MyHomePage>`.

```dart

class _MyHomePageState extends State<MyHomePage> {

  bool _amplifyConfigured = false;

  @override
  initState() {
    super.initState();
    _configureAmplify();
  }

  void _configureAmplify() async {

    Amplify.addPlugin(AmplifyAPI()); // UNCOMMENT this line once backend is deployed
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
}
```
