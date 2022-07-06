:::NEW_COMMAND:::
:::CREATE:::

```dart
Future<void> create:::MODEL:::() async {
  try {
    final model = :::MODEL:::(name: 'my first :::MODEL:::', description: ':::MODEL::: description');
    final request = ModelMutations.create(model);
    final response = await Amplify.API.mutate(request: request).response;

    final created:::MODEL::: = response.data;
    if (created:::MODEL::: == null) {
      safePrint('errors: ${response.errors}');
      return;
    }
    safePrint('Mutation result: ${created:::MODEL:::.name}');
  } on ApiException catch (e) {
    safePrint('Mutation failed: $e');
  }
}
```

:::NEW_COMMAND:::
:::UPDATE:::

```dart
Future<void> update:::MODEL:::(:::MODEL::: original:::MODEL:::) async {
  final modelWithNewName = original:::MODEL:::.copyWith(name: 'new name');

  final request = ModelMutations.update(modelWithNewName);
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
  final request = ModelMutations.deleteById(Todo.classType, 'ENTER ID HERE');
  final response = await Amplify.API.mutate(request: request).response;
  print('Response: $response');
}
```

:::NEW_COMMAND:::
:::QUERY:::

```dart
Future<Todo?> queryItem(:::MODEL::: queried:::MODEL:::) async {
   try {
      final request = ModelQueries.get(Todo.classType, queried:::MODEL:::.id);
      final response = await Amplify.API.query(request: request).response;
      final model = response.data;
      if (model == null) {
        print('errors: ${response.errors}');
      }
      return model;
   } on ApiException catch (e) {
      print('Query failed: $e');
      return null;
   }
}
```
