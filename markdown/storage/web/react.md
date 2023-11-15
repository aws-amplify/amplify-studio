:::NEW_COMMAND:::
UPLOAD_PUBLIC
```js
import { uploadData } from 'aws-amplify/storage';

try {
  const result = await uploadData({
    key: filename,
    data: file
  }).result;
  console.log('Succeeded: ', result);
} catch (error) {
  console.log('Error : ', error);
}
```
:::NEW_COMMAND:::
UPLOAD_PROTECTED
```js
import { uploadData } from 'aws-amplify/storage';

try {
  const result = await uploadData({
    key: filename,
    data: file,
    options: {
        accessLevel: 'protected'
    }
  }).result;
  console.log('Succeeded: ', result);
} catch (error) {
  console.log('Error : ', error);
}
```
:::NEW_COMMAND:::
UPLOAD_PRIVATE
```js
import { uploadData } from 'aws-amplify/storage';

try {
  const result = await uploadData({
    key: filename,
    data: file,
    options: {
        accessLevel: 'private'
    }
  }).result;
  console.log('Succeeded: ', result);
} catch (error) {
  console.log('Error : ', error);
}
```
:::NEW_COMMAND:::
DOWNLOAD_PUBLIC
```js
import { getUrl } from 'aws-amplify/storage';

const getUrlResult = await getUrl({
  key: filename,
});
```
:::NEW_COMMAND:::
DOWNLOAD_PROTECTED
```js
import { getUrl } from 'aws-amplify/storage';

const getUrlResult = await getUrl({
  key: filename,
  options: {
    accessLevel: 'protected' 
  }
});
```
:::NEW_COMMAND:::
DOWNLOAD_PRIVATE
```js
import { getUrl } from 'aws-amplify/storage';

const getUrlResult = await getUrl({
  key: filename,
  options: {
    accessLevel: 'private' 
  }
});
```
:::NEW_COMMAND:::
LIST_PUBLIC
```js
import { list } from 'aws-amplify/storage';

try {
  const result = await list({
    prefix: 'photos/'
  });
} catch (error) {
  console.log(error);
}
```
:::NEW_COMMAND:::
LIST_PROTECTED
```js
import { list } from 'aws-amplify/storage';

try {
  const result = await list({
    prefix: 'photos/',
    options: {
      accessLevel: 'protected'
    }
  });
} catch (error) {
  console.log(error);
}
```
:::NEW_COMMAND:::
LIST_PRIVATE
```js
import { list } from 'aws-amplify/storage';

try {
  const response = await list({
    prefix: 'photos/',
    options:  {
        accessLevel: 'private',
    }
  })
  console.log('Listed Items:', response.items);
} catch(error) {
  console.log('Error ': error);
}

```
:::NEW_COMMAND:::
REMOVE_PUBLIC
```js
import { remove } from 'aws-amplify/storage';

try {
  await remove({ key: filename });
} catch (error) {
  console.log('Error ', error);
}
```
:::NEW_COMMAND:::
REMOVE_PROTECTED
```js
import { remove } from 'aws-amplify/storage';

try {
  await remove({
    key: filename,
    options: {
      accessLevel: 'protected'
    }
  });
} catch (error) {
  console.log('Error ', error);
}
```
:::NEW_COMMAND:::
REMOVE_PRIVATE
```js
import { remove } from 'aws-amplify/storage';

try {
  await remove({
    key: filename,
    options: {
      accessLevel: 'private'
    }
  });
} catch (error) {
  console.log('Error ', error);
}
```