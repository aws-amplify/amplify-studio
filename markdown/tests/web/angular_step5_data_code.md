:::NEW_COMMAND:::
:::CREATE:::
```js
import { DataStore } from '@aws-amplify/datastore';
import { :::MODEL::: } from './models';
```
```js
:::NO_COPY:::
...
```
```js
await DataStore.save(
    new :::MODEL:::({:::FIELDS:::})
);
```
:::NEW_COMMAND:::
:::UPDATE:::
```js
import { DataStore } from '@aws-amplify/datastore';
import { :::MODEL::: } from './models';
```
```js
:::NO_COPY:::
...
```
```js
/* Models in DataStore are immutable. To update a record you must use the copyOf function
 to apply updates to the item’s fields rather than mutating the instance directly */
await DataStore.save(:::MODEL:::.copyOf(CURRENT_ITEM, item => {
    // Update the values on {item} variable to update DataStore entry
}));
```
:::NEW_COMMAND:::
:::DELETE:::
```js
import { DataStore } from '@aws-amplify/datastore';
import { :::MODEL::: } from './models';
```
```js
:::NO_COPY:::
...
```
```js
const modelToDelete = await DataStore.query(:::MODEL:::, 123456789);
DataStore.delete(modelToDelete);
```
:::NEW_COMMAND:::
:::QUERY:::
```js
import { DataStore } from '@aws-amplify/datastore';
import { :::MODEL::: } from './models';
```
```js
:::NO_COPY:::
...
```
```js
const models = await DataStore.query(:::MODEL:::);
console.log(models);
```