:::NEW_COMMAND:::
UPLOAD_PUBLIC
```dart
import 'dart:io';
import 'package:path_provider/path_provider.dart';

Future<void> createAndUploadFile() async {
  // Create a dummy file
  final exampleString = 'Example file contents';
  final tempDir = await getTemporaryDirectory();
  final exampleFile = File(tempDir.path + '/test.txt')
    ..createSync()
    ..writeAsStringSync(exampleString);

  // Upload the file to S3
  try {
    final UploadFileResult result = await Amplify.Storage.uploadFile(
      local: exampleFile,
      key: 'ExampleKey',
    );
    print('Successfully uploaded file: \${result.key}');
  } on StorageException catch (e) {
    print('Error uploading file: $e');
  }
}
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```dart
// code here
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```dart
// code here
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```dart
import 'dart:io';
import 'package:path_provider/path_provider.dart';

Future<void> downloadFile() async {
  final documentsDir = await getApplicationDocumentsDirectory();
  final filepath = documentsDir.path + '/test.txt';
  final file = File(filepath);

  try {
    await Amplify.Storage.downloadFile(
      key: 'ExampleKey', 
      local: file
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
// code here
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```dart
// code here
```
:::NEW_COMMAND:::
LIST_PUBLIC
```dart
// You can list all of the objects uploaded under a given prefix. This will list all public files (i.e. those with guest access level)
Future<void> listItems() async {
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
// code here
```
:::NEW_COMMAND:::
LIST_PRIVATE
```dart
// code here
```
:::NEW_COMMAND:::
REMOVE_PUBLIC
```dart
Future<void> deleteFile() async {
    try {
        final RemoveResult result =
            await Amplify.Storage.remove(key: 'ExampleKey'); //specify the key
        print('Deleted file: \${result.key}');
    } on StorageException catch (e) {
        print('Error deleting file: $e');
    }
}
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```dart
// code here
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```dart
// code here
```