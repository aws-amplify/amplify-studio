:::NEW_COMMAND:::
UPLOAD_PUBLIC
```swift
import Amplify

do {
    let dataString = "MyData"
    let data = Data(dataString.utf8)
    let uploadTask = try await Amplify.Storage.uploadData(
        key: "ExampleKey",
        data: data
    )
    
    Task {
        for await progress in await uploadTask.progress {
            print("Progress: \(progress)")
        }
    }
    
    let value = try await uploadTask.value
    print("Completed: \(value)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```swift
import Amplify

do {
    let dataString = "MyData"
    let data = Data(dataString.utf8)
    let options = StorageUploadDataRequest.Options(accessLevel: .protected)
    let uploadTask = try await Amplify.Storage.uploadData(
        key: "ExampleKey",
        data: data,
        options: options
    )
    
    Task {
        for await progress in await uploadTask.progress {
            print("Progress: \(progress)")
        }
    }
    
    let value = try await uploadTask.value
    print("Completed: \(value)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```swift
import Amplify

do {
    let dataString = "MyData"
    let data = Data(dataString.utf8)
    let options = StorageUploadDataRequest.Options(accessLevel: .private)
    let uploadTask = try await Amplify.Storage.uploadData(
        key: "ExampleKey",
        data: data,
        options: options
    )

    Task {
        for await progress in await uploadTask.progress {
            print("Progress: \(progress)")
        }
    }

    let value = try await uploadTask.value
    print("Completed: \(value)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```swift
import Amplify

do {
    let downloadTask = try await Amplify.Storage.downloadData(
        key: "ExampleKey"
    )

    Task {
        for await progress in await downloadTask.progress {
            print("Progress: \(progress)")
        }
    }

    let value = try await downloadTask.value
    print("Completed: \(value)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```swift
import Amplify

do {
    let dataString = "MyData"
    let data = Data(dataString.utf8)
    let options = StorageDownloadDataRequest.Options(accessLevel: .protected)
    let downloadTask = try await Amplify.Storage.downloadData(
        key: "ExampleKey",
        options: options
    )

    Task {
        for await progress in await downloadTask.progress {
            print("Progress: \(progress)")
        }
    }

    let value = try await downloadTask.value
    print("Completed: \(value)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```swift
import Amplify

do {
    let options = StorageDownloadDataRequest.Options(accessLevel: .private)
    let downloadTask = try await Amplify.Storage.downloadData(
        key: "ExampleKey",
        options: options
    )

    Task {
        for await progress in await downloadTask.progress {
            print("Progress: \(progress)")
        }
    }

    let value = try await downloadTask.value
    print("Completed: \(value)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
LIST_PUBLIC
```swift
import Amplify

do {
    let listResult = try await Amplify.Storage.list()
    print("Completed")
    listResult.items.forEach { item in
        print("Key: \(item.key)")
    }
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
LIST_PROTECTED
```swift
import Amplify

do {
    let options = StorageListRequest.Options(accessLevel: .protected)
    let listResult = try await Amplify.Storage.list(options: options)
    print("Completed")
    listResult.items.forEach { item in
        print("Key: \(item.key)")
    }
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
LIST_PRIVATE
```swift
import Amplify

do {
    let options = StorageListRequest.Options(accessLevel: .private)
    let listResult = try await Amplify.Storage.list(options: options)
    print("Completed")
    listResult.items.forEach { item in
        print("Key: \(item.key)")
    }
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
REMOVE_PUBLIC
```swift
import Amplify

do {
    let removedKey = try await Amplify.Storage.remove(key: "ExampleKey")
    print("Deleted \(removedKey)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```swift
import Amplify

do {
    let options = StorageRemoveRequest.Options(accessLevel: .protected)
    let removedKey = try await Amplify.Storage.remove(key: "ExampleKey")
    print("Deleted \(removedKey)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```swift
import Amplify

do {
    let options = StorageRemoveRequest.Options(accessLevel: .private)
    let removedKey = try await Amplify.Storage.remove(key: "ExampleKey")
    print("Deleted \(removedKey)")
} catch let error as StorageError {
    print("Failed: \(error.errorDescription). \(error.recoverySuggestion)")
} catch {
    print("Unexpected error: \(error)")
}
```