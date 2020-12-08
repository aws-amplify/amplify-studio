Pull in the latest backend information into your app's code base. 

1. Open your Terminal and run the following command:
```bash
:::AMPLIFY_PULL_COMMAND:::
```

2. Make sure to add a new `AWSApiPlugin()` and configure `Amplify`.
```kt
:::NO_COPY:::
try {
```
```kt
    Amplify.addPlugin(AWSApiPlugin())
```
```kt
:::NO_COPY:::
    Amplify.addPlugin(AWSDataStorePlugin())
    Amplify.configure(applicationContext)
    Log.i("Amplify", "Initialized Amplify")
} catch (e: AmplifyException) {
    Log.e("Amplify", "Could not initialize Amplify", e)
}
```