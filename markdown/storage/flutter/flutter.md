:::NEW_COMMAND:::
UPLOAD_PUBLIC
```dart
Future<void> createAndUploadFilePublic() async {
  // Create a dummy file
  final exampleString = 'Example file contents';
  final tempDir = await getTemporaryDirectory();
  final exampleFile = File(tempDir.path + '/example.txt')
    ..createSync()
    ..writeAsStringSync(exampleString);
  // Upload the file to S3
  try {
    final UploadFileResult result = await Amplify.Storage.uploadFile(
      local: exampleFile,
      key: 'ExampleKey',
      options: S3UploadFileOptions(
        accessLevel: StorageAccessLevel.guest,
      ),
    );
    print('Successfully uploaded file: ${result.key}');
  } on StorageException catch (e) {
    print('Error uploading file: $e');
  }
}
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```dart
Future<void> createAndUploadFileProtected() async {
  // Create a dummy file
  final exampleString = 'Example file contents';
  final tempDir = await getTemporaryDirectory();
  final exampleFile = File(tempDir.path + '/example.txt')
    ..createSync()
    ..writeAsStringSync(exampleString);
  // Upload the file to S3
  try {
    final UploadFileResult result = await Amplify.Storage.uploadFile(
      local: exampleFile,
      key: 'ExampleKey',
      options: S3UploadFileOptions(
        accessLevel: StorageAccessLevel.protected,
      ),
    );
    print('Successfully uploaded file: ${result.key}');
  } on StorageException catch (e) {
    print('Error uploading file: $e');
  }
}
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```dart
Future<void> createAndUploadFilePrivate() async {
  // Create a dummy file
  final exampleString = 'Example file contents';
  final tempDir = await getTemporaryDirectory();
  final exampleFile = File(tempDir.path + '/example.txt')
    ..createSync()
    ..writeAsStringSync(exampleString);
  // Upload the file to S3
  try {
    final UploadFileResult result = await Amplify.Storage.uploadFile(
      local: exampleFile,
      key: 'ExampleKey',
      options: S3UploadFileOptions(
        accessLevel: StorageAccessLevel.private,
      ),
    );
    print('Successfully uploaded file: ${result.key}');
  } on StorageException catch (e) {
    print('Error uploading file: $e');
  }
}
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```dart
Future<void> downloadFilePublic() async {
  final documentsDir = await getApplicationDocumentsDirectory();
  final filepath = documentsDir.path + '/example.txt';
  final file = File(filepath);
  try {
    await Amplify.Storage.downloadFile(
      key: 'ExampleKey',
      local: file,
    );
    final String contents = file.readAsStringSync();
    print('Downloaded contents: $contents');
  } on StorageException catch (e) {
    print('Error downloading file: $e');
  }
}

```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```dart
Future<void> downloadFileProtected() async {
  final documentsDir = await getApplicationDocumentsDirectory();
  final filepath = documentsDir.path + '/example.txt';
  final file = File(filepath);
  try {
    await Amplify.Storage.downloadFile(
      key: 'ExampleKey',
      local: file,
      options: DownloadFileOptions(
        accessLevel: StorageAccessLevel.protected,
        // e.g. us-west-2:2f41a152-14d1-45ff-9715-53e20751c7ee
        targetIdentityId: cognitoIdentityId,
      ),
    );
    final String contents = file.readAsStringSync();
    print('Downloaded contents: $contents');
  } on StorageException catch (e) {
    print('Error downloading file: $e');
  }
}
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```dart
Future<void> downloadFilePrivate() async {
  final documentsDir = await getApplicationDocumentsDirectory();
  final filepath = documentsDir.path + '/example.txt';
  final file = File(filepath);
  try {
    await Amplify.Storage.downloadFile(
      key: 'ExampleKey',
      local: file,
      options: DownloadFileOptions(
        accessLevel: StorageAccessLevel.private,
        // e.g. us-west-2:2f41a152-14d1-45ff-9715-53e20751c7ee
        targetIdentityId: cognitoIdentityId,
      ),
    );
    final String contents = file.readAsStringSync();
    print('Downloaded contents: $contents');
  } on StorageException catch (e) {
    print('Error downloading file: $e');
  }
}
```
:::NEW_COMMAND:::
LIST_PUBLIC
```dart
Future<void> listItemsPublic() async {
  try {
    final ListResult result = await Amplify.Storage.list();
    final List<StorageItem> items = result.items;
    print('Got items: $items');
  } on StorageException catch (e) {
    print('Error listing items: $e');
  }
}

```
:::NEW_COMMAND:::
LIST_PROTECTED
```dart
Future<void> listItemsProtected() async {
  try {
    final ListResult result = await Amplify.Storage.list(
        options: ListOptions(
        accessLevel: StorageAccessLevel.protected,
        // e.g. us-west-2:2f41a152-14d1-45ff-9715-53e20751c7ee
        targetIdentityId: cognitoIdentityId,
      ),
    );
    final List<StorageItem> items = result.items;
    print('Got items: $items');
  } on StorageException catch (e) {
    print('Error listing items: $e');
  }
}
```
:::NEW_COMMAND:::
LIST_PRIVATE
```dart
Future<void> listItemsPrivate() async {
  try {
    final ListResult result = await Amplify.Storage.list(
        options: ListOptions(
        accessLevel: StorageAccessLevel.private,
        // e.g. us-west-2:2f41a152-14d1-45ff-9715-53e20751c7ee
        targetIdentityId: cognitoIdentityId,
      ),
    );
    final List<StorageItem> items = result.items;
    print('Got items: $items');
  } on StorageException catch (e) {
    print('Error listing items: $e');
  }
}
```
:::NEW_COMMAND:::
REMOVE_PUBLIC
```dart
Future<void> deleteFilePublic() async {
  try {
    final RemoveResult result =
        await Amplify.Storage.remove(key: 'ExampleKey');
    print('Deleted file: ${result.key}');
  } on StorageException catch (e) {
    print('Error deleting file: $e');
  }
}
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```dart
Future<void> deleteFileProtected() async {
  try {
    final RemoveResult result = await Amplify.Storage.remove(
      key: 'ExampleKey',
      options: RemoveOptions(
        accessLevel: StorageAccessLevel.protected,
      ),
    );
    print('Deleted file: ${result.key}');
  } on StorageException catch (e) {
    print('Error deleting file: $e');
  }
}
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```dart
Future<void> deleteFilePrivate() async {
  try {
    final RemoveResult result = await Amplify.Storage.remove(
      key: 'ExampleKey',
      options: RemoveOptions(
        accessLevel: StorageAccessLevel.private,
      ),
    );
    print('Deleted file: ${result.key}');
  } on StorageException catch (e) {
    print('Error deleting file: $e');
  }
}
```