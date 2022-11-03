:::NEW_COMMAND:::
:::CREATE:::

```kt
val model = :::MODEL:::.builder()
    :::FIELDS:::
    .build()

Amplify.API.mutate(ModelMutation.create(model),
    { Log.i("MyAmplifyApp", ":::MODEL::: with id: ${it.data.id}") }
    { Log.e("MyAmplifyApp", "Create failed", it) }
)
```

:::NEW_COMMAND:::
:::UPDATE:::

```kt
Amplify.API.mutate(ModelMutation.update(updatedModel),
    { Log.i("MyAmplifyApp", ":::MODEL::: with id: ${it.data.id}") }
    { Log.e("MyAmplifyApp", "Update failed", it) }
)
```

:::NEW_COMMAND:::
:::DELETE:::

```kt
Amplify.API.mutate(ModelMutation.delete(modelToBeDeleted),
    { Log.i("MyAmplifyApp", ":::MODEL::: with id: ${it.data.id}") }
    { Log.e("MyAmplifyApp", "Deletion failed", it) }
)
```

:::NEW_COMMAND:::
:::QUERY:::

```kt
Amplify.API.query(ModelQuery.get(:::MODEL:::::class.java, "YOUR_RECORD_ID"),
    { Log.i("MyAmplifyApp", "Query results = ${(it.data as :::MODEL:::).id}") },
    { Log.e("MyAmplifyApp", "Query failed", it) }
);
```
