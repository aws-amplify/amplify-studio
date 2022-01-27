:::NEW_COMMAND:::
UPLOAD_PUBLIC
```java
private void uploadFile() {
    File exampleFile = new File(getApplicationContext().getFilesDir(), "ExampleKey");

    try {
        BufferedWriter writer = new BufferedWriter(new FileWriter(exampleFile));
        writer.append("Example file contents");
        writer.close();
    } catch (Exception exception) {
        Log.e("MyAmplifyApp", "Upload failed", exception);
    }

    Amplify.Storage.uploadFile(
            "ExampleKey",
            exampleFile,
            result -> Log.i("MyAmplifyApp", "Successfully uploaded: " + result.getKey()),
            storageFailure -> Log.e("MyAmplifyApp", "Upload failed", storageFailure)
    );
}
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```java
// code here
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```java
// code here
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```java
Amplify.Storage.downloadFile(
    "ExampleKey",
    new File(getApplicationContext().getFilesDir() + "/test.txt"),
    result -> Log.i("MyAmplifyApp", "Successfully downloaded: " + result.getFile().getName()),
    error -> Log.e("MyAmplifyApp",  "Download Failure", error)
);
```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```java
// code here
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```java
// code here
```
:::NEW_COMMAND:::
LIST_PUBLIC
```java
Amplify.Storage.list("/",
    result -> {
        for (StorageItem item : result.getItems()) {
            Log.i("MyAmplifyApp", "Item: " + item.getKey());
        }
    },
    error -> Log.e("MyAmplifyApp", "List failure", error)
);
```
:::NEW_COMMAND:::
LIST_PROTECTED
```java
StorageListOptions options = StorageListOptions.builder()
    .accessLevel(StorageAccessLevel.PROTECTED)
    .targetIdentityId("otherUserID")
    .build();

Amplify.Storage.list(
    "/",
    options,
    result -> {
        for (StorageItem item : result.getItems()) {
            Log.i("MyAmplifyApp", "Item: " + item.getKey());
        }
    },
    error -> Log.e("MyAmplifyApp", "List failure", error)
);
```
:::NEW_COMMAND:::
LIST_PRIVATE
```java
StorageListOptions options = StorageListOptions.builder()
    .accessLevel(StorageAccessLevel.PRIVATE)
    .targetIdentityId("otherUserID")
    .build();

Amplify.Storage.list(
    "/",
    options,
    result -> {
        for (StorageItem item : result.getItems()) {
            Log.i("MyAmplifyApp", "Item: " + item.getKey());
        }
    },
    error -> Log.e("MyAmplifyApp", "List failure", error)
);
```
:::NEW_COMMAND:::
REMOVE_PUBLIC
```java
Amplify.Storage.remove(
    "test.txt",
    result -> Log.i("MyAmplifyApp", "Successfully removed: " + result.getKey()),
    error -> Log.e("MyAmplifyApp", "Remove failure", error)
);
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```java
// code here
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```java
// code here
```