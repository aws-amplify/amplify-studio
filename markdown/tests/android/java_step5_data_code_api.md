:::NEW_COMMAND:::
:::CREATE:::

```java
:::MODEL::: model = :::MODEL:::.builder()
    :::FIELDS:::
    .build();

Amplify.API.mutate(ModelMutation.create(model),
    response -> Log.i("MyAmplifyApp", ":::MODEL::: with id: " + response.getData().getId()),
    error -> Log.e("MyAmplifyApp", "Create failed", error)
);
```

:::NEW_COMMAND:::
:::UPDATE:::

```java
Amplify.API.mutate(ModelMutation.update(updatedModel),
    response -> Log.i("MyAmplifyApp", ":::MODEL::: with id: " + response.getData().getId()),
    error -> Log.e("MyAmplifyApp", "Update failed", error)
);
```

:::NEW_COMMAND:::
:::DELETE:::

```java
Amplify.API.mutate(ModelMutation.delete(modelToBeDeleted),
    response -> Log.i("MyAmplifyApp", ":::MODEL::: with id: " + response.getData().getId()),
    error -> Log.e("MyAmplifyApp", "Deletion failed", error)
);
```

:::NEW_COMMAND:::
:::QUERY:::

```java
Amplify.API.query(
    ModelQuery.get(:::MODEL:::.class, "YOUR_RECORD_ID"),
    response -> Log.i("MyAmplifyApp", ((:::MODEL:::) response.getData()).getId()),
    error -> Log.e("MyAmplifyApp", error.toString(), error)
);
```
