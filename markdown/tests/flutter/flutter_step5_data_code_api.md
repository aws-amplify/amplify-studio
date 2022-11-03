:::NEW_COMMAND:::
:::CREATE:::

```dart
Future<void> create:::MODEL:::() async {
  try {
    final model = :::MODEL:::(:::FIELDS:::);
    final request = ModelMutations.create(model);
    final response = await Amplify.API.mutate(request: request).response;

    final created:::MODEL::: = response.data;
    if (created:::MODEL::: == null) {
      safePrint('errors: ${response.errors}');
      return;
    }
    safePrint('Mutation result: ${created:::MODEL:::.id}');
  } on ApiException catch (e) {
    safePrint('Mutation failed: $e');
  }
}
```

:::NEW_COMMAND:::
:::UPDATE:::

```dart
Future<void> update:::MODEL:::(:::MODEL::: original:::MODEL:::) async {
  final updatedModel = original:::MODEL:::.copyWith(:::FIELDS:::);

  final request = ModelMutations.update(updatedModel);
  final response = await Amplify.API.mutate(request: request).response;
  print('Response: $response');
}
```

:::NEW_COMMAND:::
:::DELETE:::

```dart
Future<void> delete:::MODEL:::(:::MODEL::: modelToDelete) async {
  final request = ModelMutations.delete(modelToDelete);
  final response = await Amplify.API.mutate(request: request).response;
  print('Response: $response');
}

// or delete by ID, ideal if you do not have the instance in memory, yet
Future<void> delete:::MODEL:::ById(:::MODEL::: modelToDelete) async {
  final request = ModelMutations.deleteById(:::MODEL:::.classType, 'ENTER ID HERE');
  final response = await Amplify.API.mutate(request: request).response;
  print('Response: $response');
}
```

:::NEW_COMMAND:::
:::QUERY:::

```dart
Future<List<:::MODEL:::?>> queryListItems() async {
  try {
    final request = ModelQueries.list(:::MODEL:::.classType);
    final response = await Amplify.API.query(request: request).response;

    final items = response.data?.items;
    if (items == null) {
      print('errors: ${response.errors}');
      return <:::MODEL:::?>[];
    }
    return items;
  } on ApiException catch (e) {
    print('Query failed: $e');
  }
  return <:::MODEL:::?>[];
}

```
