:::NEW_COMMAND:::
:::SIGNIN:::
```
await DataStore.save(
    new :::MODEL:::(
        :::FIELDS:::
    )
);
```
:::NEW_COMMAND:::
:::SIGNOUT:::
```
await DataStore.save(
    new :::MODEL:::(
        :::FIELDS:::
    )
);
```
:::NEW_COMMAND:::
:::SIGNUP:::
```
const modelToDelete = await DataStore.query(:::MODEL:::, 123456789);
DataStore.delete(modelToDelete);
```