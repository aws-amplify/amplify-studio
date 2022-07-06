:::NEW_COMMAND:::
:::CREATE:::

```java
:::MODEL::: model = :::MODEL:::.builder()
    .name("My :::MODEL:::")
    .build();

Amplify.API.mutate(ModelMutation.create(model),
    response -> Log.i("MyAmplifyApp", ":::MODEL::: with id: " + response.getData().getId()),
    error -> Log.e("MyAmplifyApp", "Create failed", error)
);
```

:::NEW_COMMAND:::
:::UPDATE:::

```java
:::MODEL::: model = :::MODEL:::.builder()
    .name("My :::MODEL:::")
    .build();

Amplify.API.mutate(ModelMutation.update(model),
    response -> Log.i("MyAmplifyApp", ":::MODEL::: with id: " + response.getData().getId()),
    error -> Log.e("MyAmplifyApp", "Create failed", error)
);
```

:::NEW_COMMAND:::
:::DELETE:::

```java
:::MODEL::: model = :::MODEL:::.builder()
    .name("My :::MODEL:::")
    .build();

Amplify.API.mutate(ModelMutation.delete(model),
    response -> Log.i("MyAmplifyApp", ":::MODEL::: with id: " + response.getData().getId()),
    error -> Log.e("MyAmplifyApp", "Create failed", error)
);
```

:::NEW_COMMAND:::
:::QUERY:::

```java
private void get:::MODEL:::(String id) {
    Amplify.API.query(
        ModelQuery.get(:::MODEL:::.class, id),
        response -> Log.i("MyAmplifyApp", ((:::MODEL:::) response.getData()).getName()),
        error -> Log.e("MyAmplifyApp", error.toString(), error)
    );
}
```
