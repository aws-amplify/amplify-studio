:::NEW_COMMAND:::
:::CREATE:::

```kt
val model = :::MODEL:::.builder()
    .name("My :::MODEL:::")
    .build()

Amplify.API.mutate(ModelMutation.create(model),
    { Log.i("MyAmplifyApp", ":::MODEL::: with id: ${it.data.id}") }
    { Log.e("MyAmplifyApp", "Create failed", it) }
)
```

:::NEW_COMMAND:::
:::UPDATE:::

```kt
val model = :::MODEL:::.builder()
    .name("My :::MODEL:::")
    .build()

Amplify.API.mutate(ModelMutation.update(model),
    { Log.i("MyAmplifyApp", ":::MODEL::: with id: ${it.data.id}") }
    { Log.e("MyAmplifyApp", "Create failed", it) }
)
```

:::NEW_COMMAND:::
:::DELETE:::

```kt
val model = :::MODEL:::.builder()
    .name("My :::MODEL:::")
    .build()

Amplify.API.mutate(ModelMutation.delete(model),
    { Log.i("MyAmplifyApp", ":::MODEL::: with id: ${it.data.id}") }
    { Log.e("MyAmplifyApp", "Create failed", it) }
)
```

:::NEW_COMMAND:::
:::QUERY:::

```kt
private fun get:::MODEL:::(id: String) {
    Amplify.API.query(ModelQuery.get(:::MODEL:::::class.java, id),
        { Log.i("MyAmplifyApp", "Query results = ${(it.data as :::MODEL:::).name}") },
        { Log.e("MyAmplifyApp", "Query failed", it) }
    );
}
```
