Pull in the latest backend information into your app's code base. 

1. Open your Terminal and run the following command:
```bash
:::AMPLIFY_PULL_COMMAND:::
```

2. Make sure to add a `new AWSApiPlugin()` and configure `Amplify`.
```java
:::NO_COPY:::
try {
```
```java
    Amplify.addPlugin(new AWSApiPlugin());
```
```java
:::NO_COPY:::
    Amplify.addPlugin(new AWSDataStorePlugin());
    Amplify.configure(getApplicationContext());
} catch (AmplifyException error) {
    Log.e("Amplify", "Could not initialize Amplify", error);
}
```