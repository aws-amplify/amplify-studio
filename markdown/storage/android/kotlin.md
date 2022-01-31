:::NEW_COMMAND:::
UPLOAD_PUBLIC
```kt
private fun uploadFile(key: String, file: File) {
    
    Amplify.Storage.uploadFile(key, file,
        { Log.i("MyAmplifyApp", "Successfully uploaded: $key" ) },
        { error -> Log.e("MyAmplifyApp", "Upload failed", error) }
    )
}
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```kt
private fun uploadFile(key: String, file: File) {
    val options = StorageUploadFileOptions.builder()
        .accessLevel(StorageAccessLevel.PROTECTED)
        .build()
    
    Amplify.Storage.uploadFile(key, file, options,
        { Log.i("MyAmplifyApp", "Successfully uploaded: $key" ) },
        { error -> Log.e("MyAmplifyApp", "Upload failed", error) }
    )
}
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```kt
private fun uploadFile(key: String, file: File) {
    val options = StorageUploadFileOptions.builder()
        .accessLevel(StorageAccessLevel.PRIVATE)
        .build()
    
    Amplify.Storage.uploadFile(key, file, options,
        { Log.i("MyAmplifyApp", "Successfully uploaded: $key" ) },
        { error -> Log.e("MyAmplifyApp", "Upload failed", error) }
    )
}
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```kt
private fun downloadFile(file: File, key: String) {
    
    Amplify.Storage.downloadFile(key, file,
        { Log.i("MyAmplifyApp", "Successfully downloaded: $key") },
        { error -> Log.e("MyAmplifyApp", "Download failed", error) }
    )
}
```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```kt
private fun downloadFile(file: File, key: String, otherIdentityId: String) {
    val options = StorageDownloadFileOptions.builder()
        .accessLevel(StorageAccessLevel.PROTECTED)
        .targetIdentityId(otherIdentityId)
        .build()
    
    Amplify.Storage.downloadFile(key, file, options,
        { Log.i("MyAmplifyApp", "Successfully downloaded: $key") },
        { error -> Log.e("MyAmplifyApp", "Download failed", error) }
    )
}
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```kt
private fun downloadFile(file: File, key: String) {
    val options = StorageDownloadFileOptions.builder()
        .accessLevel(StorageAccessLevel.PRIVATE)
        .build()
    
    Amplify.Storage.downloadFile(key, file, options,
        { Log.i("MyAmplifyApp", "Successfully downloaded: $key") },
        { error -> Log.e("MyAmplifyApp", "Download failed", error) }
    )
}
```
:::NEW_COMMAND:::
LIST_PUBLIC
```kt
Amplify.Storage.list("",
    { result ->
        result.items.forEach { item ->
            Log.i("MyAmplifyApp", "Item: ${item.key}")
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

Amplify.Storage.list("", options,
    { result ->
        result.items.forEach { item ->
            Log.i("MyAmplifyApp", "Item: ${item.key}")
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
    .build()

Amplify.Storage.list("", options,
    { result ->
        result.items.forEach { item ->
            Log.i("MyAmplifyApp", "Item: ${item.key}")
        }
    },
    { Log.e("MyAmplifyApp", "List failure", it) }
)
```
:::NEW_COMMAND:::
REMOVE_PUBLIC
```kt
Amplify.Storage.remove("myUploadedFileName.txt",
    { Log.i("MyAmplifyApp", "Successfully removed: ${it.key}") },
    { Log.e("MyAmplifyApp", "Remove failure", it) } )
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```kt
val options = StorageRemoveOptions.builder()
    .accessLevel(StorageAccessLevel.PROTECTED)
    .targetIdentityId("otherUserID")
    .build()

Amplify.Storage.remove("myUploadedFileName.txt",
    options,
    { Log.i("MyAmplifyApp", "Successfully removed: ${it.key}") },
    { Log.e("MyAmplifyApp", "Remove failure", it) } )
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```kt
val options = StorageRemoveOptions.builder()
    .accessLevel(StorageAccessLevel.PRIVATE)
    .build()

Amplify.Storage.remove("myUploadedFileName.txt",
    options,
    { Log.i("MyAmplifyApp", "Successfully removed: ${it.key}") },
    { Log.e("MyAmplifyApp", "Remove failure", it) } )
```