:::NEW_COMMAND:::
UPLOAD_PUBLIC
```java
private void uploadFile(String key, File file) {

    Amplify.Storage.uploadFile(key, file,
        result -> Log.i("MyAmplifyApp", "Successfully uploaded: " + key),
        error -> Log.e("MyAmplifyApp", "Upload failed", error)
    );
}
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```java
private void uploadFile(String key, File file) {
    StorageUploadFileOptions options = StorageUploadFileOptions.builder()
        .accessLevel(StorageAccessLevel.PROTECTED)
        .build();

    Amplify.Storage.uploadFile(key, file, options,
        result -> Log.i("MyAmplifyApp", "Successfully uploaded: " + key),
        error -> Log.e("MyAmplifyApp", "Upload failed", error)
    );
}
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```java
private void uploadFile(String key, File file) {
    StorageUploadFileOptions options = StorageUploadFileOptions.builder()
        .accessLevel(StorageAccessLevel.PRIVATE)
        .build();

    Amplify.Storage.uploadFile(key, file, options,
        result -> Log.i("MyAmplifyApp", "Successfully uploaded: " + key),
        error -> Log.e("MyAmplifyApp", "Upload failed", error)
    );
}
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```java
private void downloadFile(String key, File file) {

    Amplify.Storage.downloadFile(key, file,
        result -> Log.i("MyAmplifyApp", "Successfully downloaded: " + key),
        error -> Log.e("MyAmplifyApp", "Download failed", error)
    );
}
```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```java
private void downloadFile(String key, File file, String otherIdentityId) {
    StorageDownloadFileOptions options = StorageDownloadFileOptions.builder()
        .accessLevel(StorageAccessLevel.PROTECTED)
        .targetIdentityId(otherIdentityId)
        .build();

    Amplify.Storage.downloadFile(key, file, options,
        result -> Log.i("MyAmplifyApp", "Successfully downloaded: " + key),
        error -> Log.e("MyAmplifyApp", "Download failed", error)
    );
}
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```java
private void downloadFile(String key, File file) {
    StorageDownloadFileOptions options = StorageDownloadFileOptions.builder()
        .accessLevel(StorageAccessLevel.PRIVATE)
        .build();

    Amplify.Storage.downloadFile(key, file, options,
        result -> Log.i("MyAmplifyApp", "Successfully downloaded: " + key),
        error -> Log.e("MyAmplifyApp", "Download failed", error)
    );
}
```
:::NEW_COMMAND:::
LIST_PUBLIC
```java
Amplify.Storage.list(
    "",
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
    "",
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
    "",
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
    "myUploadedFileName.txt",
    result -> Log.i("MyAmplifyApp", "Successfully removed: " + result.getKey()),
    error -> Log.e("MyAmplifyApp", "Remove failure", error)
);
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```java
StorageRemoveOptions options = StorageRemoveOptions.builder()
    .accessLevel(StorageAccessLevel.PROTECTED)
    .targetIdentityId("otherUserID")
    .build();

Amplify.Storage.remove(
    "myUploadedFileName.txt",
    options,
    result -> Log.i("MyAmplifyApp", "Successfully removed: " + result.getKey()),
    error -> Log.e("MyAmplifyApp", "Remove failure", error)
);
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```java
StorageRemoveOptions options = StorageRemoveOptions.builder()
    .accessLevel(StorageAccessLevel.PRIVATE)
    .targetIdentityId("otherUserID")
    .build();

Amplify.Storage.remove(
    "myUploadedFileName.txt",
    options,
    result -> Log.i("MyAmplifyApp", "Successfully removed: " + result.getKey()),
    error -> Log.e("MyAmplifyApp", "Remove failure", error)
);
```