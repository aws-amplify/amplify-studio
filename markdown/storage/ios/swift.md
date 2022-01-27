:::NEW_COMMAND:::
UPLOAD_PUBLIC
```swift
let dataString = "My Data"
let fileNameKey = "test.txt"
let filename = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0]
    .appendingPathComponent(fileNameKey)
do {
    try dataString.write(to: filename, atomically: true, encoding: String.Encoding.utf8)
} catch {
    print("Failed to write to file \(error)")
}

let storageOperation = Amplify.Storage.uploadFile(
    key: fileNameKey,
    local: filename,
    progressListener: { progress in
        print("Progress: \(progress)")
    }, resultListener: { event in
        switch event {
        case let .success(data):
            print("Completed: \(data)")
        case let .failure(storageError):
            print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
        }
    }
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```swift
// code here
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```swift
// code here
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```swift
let downloadToFileName = FileManager.default.urls(for: .documentDirectory,
            in: .userDomainMask)[0]
            .appendingPathComponent("test.txt")

let storageOperation = Amplify.Storage.downloadFile(
    key: "myKey",
    local: downloadToFileName,
    progressListener: { progress in
        print("Progress: \(progress)")
    }, resultListener: { event in
        switch event {
        case .success:
            print("Completed")
        case .failure(let storageError):
            print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
        }
    })
```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```swift
// code here
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```swift
// code here
```
:::NEW_COMMAND:::
LIST_PUBLIC
```swift
Amplify.Storage.list { event in
    switch event {
    case let .success(listResult):
        print("Completed")
        listResult.items.forEach { item in
            print("Key: \(item.key)")
        }
    case let .failure(storageError):
        print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
    }
}
```
:::NEW_COMMAND:::
LIST_PROTECTED
```swift
// code here
```
:::NEW_COMMAND:::
LIST_PRIVATE
```swift
// code here
```
:::NEW_COMMAND:::
REMOVE_PUBLIC
```swift
Amplify.Storage.remove(key: "myKey") { event in
    switch event {
    case let .success(data):
        print("Completed: Deleted \(data)")
    case let .failure(storageError):
        print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
    }
}
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```swift
// code here
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```swift
// code here
```