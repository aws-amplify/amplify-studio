:::NEW_COMMAND:::
:::UPLOAD-PUBLIC:::
```js
await Storage.put("test.txt", "Hello");
```
:::NEW_COMMAND:::
:::UPLOAD-PROTECTED:::
```js
await Storage.put('test.txt', 'Protected Content', {
    level: 'protected',
    contentType: 'text/plain'
});
```
:::NEW_COMMAND:::
:::UPLOAD-PRIVATE:::
```js
await Storage.put('test.txt', 'Private Content', {
    level: 'private',
    contentType: 'text/plain'
});
```
:::NEW_COMMAND:::
:::DOWNLOAD-PUBLIC:::
```js
await Storage.get('test.txt', { 
    level: 'public'
});
```
:::NEW_COMMAND:::
:::DOWNLOAD-PROTECTED:::
```js
await Storage.get('test.txt', { 
    level: 'protected'
    identityId: 'xxxxxxx' // The identityId of that user. Omit to get current user's objects.
});
```
:::NEW_COMMAND:::
:::DOWNLOAD-PRIVATE:::
```js
await Storage.get('test.txt', { 
    level: 'private'
});
```
:::NEW_COMMAND:::
:::LIST-PUBLIC:::
```js
Storage.list('photos/') // for listing ALL files without prefix, pass '' instead
        .then(result => console.log(result))
        .catch(err => console.log(err));
```
:::NEW_COMMAND:::
:::LIST-PROTECTED:::
```js
Storage.list('photos/', { 
        level: 'protected', 
        identityId: 'xxxxxxx' // The identityId of that user. Omit to get current user's objects.
    })
    .then(result => console.log(result))
    .catch(err => console.log(err));
```
:::NEW_COMMAND:::
:::LIST-PRIVATE:::
```js
Storage.list('photos/', { level: 'private' })
        .then(result => console.log(result))
        .catch(err => console.log(err));
```
:::NEW_COMMAND:::
:::REMOVE-PUBLIC:::
```js
await Storage.remove('test.txt');
```
:::NEW_COMMAND:::
:::REMOVE-PROTECTED:::
```js
await Storage.remove('test.txt', { level: 'protected' });
```
:::NEW_COMMAND:::
:::REMOVE-PRIVATE:::
```js
await Storage.remove('test.txt', { level: 'private' });
```