:::NEW_COMMAND:::
UPLOAD_PUBLIC
```kt
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
```kt
// code here
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```kt
// code here
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```kt
val file = File("\${applicationContext.filesDir}/test.txt")
Amplify.Storage.downloadFile("ExampleKey", file,
    { Log.i("MyAmplifyApp", "Successfully downloaded: \${it.file.name}") },
    { Log.e("MyAmplifyApp",  "Download Failure", it) }
)
```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```kt
// code here
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```kt
// code here
```
:::NEW_COMMAND:::
LIST_PUBLIC
```kt
Amplify.Storage.list("/",
    { result ->
        result.items.forEach { item ->
            Log.i("MyAmplifyApp", "Item: \${item.key}")
        }
    },
    { Log.e("MyAmplifyApp", "List failure", it) }
)
```
:::NEW_COMMAND:::
LIST_PROTECTED
```kt
val options = StorageListOptions.builder()
    .accessLevel(StorageAccessLevel.PROTECTED)
    .targetIdentityId("otherUserID")
    .build()

Amplify.Storage.list("/", options,
    { result ->
        result.items.forEach { item ->
            Log.i("MyAmplifyApp", "Item: \${item.key}")
        }
    },
    { Log.e("MyAmplifyApp", "List failure", it) }
)
```
:::NEW_COMMAND:::
LIST_PRIVATE
```kt
val options = StorageListOptions.builder()
    .accessLevel(StorageAccessLevel.PRIVATE)
    .targetIdentityId("otherUserID")
    .build()

Amplify.Storage.list("/", options,
    { result ->
        result.items.forEach { item ->
            Log.i("MyAmplifyApp", "Item: \${item.key}")
        }
    },
    { Log.e("MyAmplifyApp", "List failure", it) }
)
```
:::NEW_COMMAND:::
REMOVE_PUBLIC
```kt
Amplify.Storage.remove("test.txt", 
    { Log.i("MyAmplifyApp", "Successfully removed: \${it.key}") }, 
    { Log.e("MyAmplifyApp", "Remove failure", it) } 
)
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```kt
// code here
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```kt
// code here
```