:::NEW_COMMAND:::
UPLOAD_PUBLIC
```swift
import Amplify
import AWSS3StoragePlugin

let dataString = "My Data"
let data = dataString.data(using: .utf8)!
let storageOperation = Amplify.Storage.uploadData(
    key: "ExampleKey",
    data: data,
    progressListener: { progress in
        print("Progress: \(progress)")
    }, resultListener: { event in
        switch event {
        case .success(let data):
            print("Completed: \(data)")
        case .failure(let storageError):
            print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
        }
    }
)
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```swift
import Amplify
import AWSS3StoragePlugin

let dataString = "My Data"
let data = dataString.data(using: .utf8)!
let options = StorageUploadDataRequest.Options(accessLevel: .protected)
let storageOperation = Amplify.Storage.uploadData(
    key: "ExampleKey",
    data: data,
    options: options,
    progressListener: { progress in
        print("Progress: \(progress)")
    }, resultListener: { event in
        switch event {
        case .success(let data):
            print("Completed: \(data)")
        case .failure(let storageError):
            print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
        }
    }
)
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```swift
import Amplify
import AWSS3StoragePlugin

let dataString = "My Data"
let data = dataString.data(using: .utf8)!
let options = StorageUploadDataRequest.Options(accessLevel: .private)
let storageOperation = Amplify.Storage.uploadData(
    key: "ExampleKey",
    data: data,
    options: options,
    progressListener: { progress in
        print("Progress: \(progress)")
    }, resultListener: { event in
        switch event {
        case .success(let data):
            print("Completed: \(data)")
        case .failure(let storageError):
            print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
        }
    }
)
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```swift
import Amplify
import AWSS3StoragePlugin

let storageOperation = Amplify.Storage.downloadData(
    key: "myKey", 
    progressListener: { progress in
        print("Progress: \(progress)")
    }, resultListener: { (event) in
        switch event {
        case let .success(data):
            print("Completed: \(data)")
        case let .failure(storageError):
            print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
    }
})
```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```swift
import Amplify
import AWSS3StoragePlugin

let options = StorageDownloadDataRequest.Options(accessLevel: .protected)
let storageOperation = Amplify.Storage.downloadData(
    key: "myKey",
    options: options,
    progressListener: { progress in
        print("Progress: \(progress)")
    }, resultListener: { (event) in
        switch event {
        case let .success(data):
            print("Completed: \(data)")
        case let .failure(storageError):
            print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
    }
})
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```swift
import Amplify
import AWSS3StoragePlugin

let options = StorageDownloadDataRequest.Options(accessLevel: .private)
let storageOperation = Amplify.Storage.downloadData(
    key: "myKey",
    options: options,
    progressListener: { progress in
        print("Progress: \(progress)")
    }, resultListener: { (event) in
        switch event {
        case let .success(data):
            print("Completed: \(data)")
        case let .failure(storageError):
            print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
    }
})
```
:::NEW_COMMAND:::
LIST_PUBLIC
```swift
import Amplify
import AWSS3StoragePlugin

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
import Amplify
import AWSS3StoragePlugin

let options = StorageListRequest.Options(accessLevel: .protected)
Amplify.Storage.list(options: options) { event in
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
LIST_PRIVATE
```swift
import Amplify
import AWSS3StoragePlugin

let options = StorageListRequest.Options(accessLevel: .private)
Amplify.Storage.list(options: options) { event in
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
REMOVE_PUBLIC
```swift
import Amplify
import AWSS3StoragePlugin

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
import Amplify
import AWSS3StoragePlugin

let options = StorageRemoveRequest.Options(accessLevel: .protected)
Amplify.Storage.remove(key: "myKey", options: options) { event in
    switch event {
    case let .success(data):
        print("Completed: Deleted \(data)")
    case let .failure(storageError):
        print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
    }
}
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```swift
import Amplify
import AWSS3StoragePlugin

let options = StorageRemoveRequest.Options(accessLevel: .private)
Amplify.Storage.remove(key: "myKey", options: options) { event in
    switch event {
    case let .success(data):
        print("Completed: Deleted \(data)")
    case let .failure(storageError):
        print("Failed: \(storageError.errorDescription). \(storageError.recoverySuggestion)")
    }
}
```