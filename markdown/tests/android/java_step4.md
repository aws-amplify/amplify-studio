Amplify dependencies are installed through Gradle.

Under Gradle Scripts, open **build.gradle (Module: app)**.

```gradle
:::NO_COPY:::
android {

```
```gradle
    compileOptions {
        // Support for Java 8 features
        coreLibraryDesugaringEnabled true
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
```
```gradle
:::NO_COPY:::
}

dependencies {
```
```gradle
    // Amplify plugins
    implementation 'com.amplifyframework:aws-api:1.6.5'
    implementation 'com.amplifyframework:aws-datastore:1.6.5'

    // Support for Java 8 features
    coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:1.0.10'
```
```gradle
:::NO_COPY:::
}
```

Click on `Sync now`


Open your **MainActivity.java** and add the following lines to initialize Amplify libraries:
```java
:::NO_COPY:::
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
```
```java
        try {
            //Amplify.addPlugin(new AWSApiPlugin()); // UNCOMMENT this line once backend is deployed
            Amplify.addPlugin(new AWSDataStorePlugin());
            Amplify.configure(getApplicationContext());
            Log.i("Amplify", "Initialized Amplify");
        } catch (AmplifyException error) {
            Log.e("Amplify", "Could not initialize Amplify", error);
        }
```
```java
:::NO_COPY:::
    }
}
```