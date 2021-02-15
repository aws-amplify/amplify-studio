:::NEW_COMMAND:::
:::CREATE:::

```dart
final item = :::MODEL:::(:::FIELDS:::);
await Amplify.DataStore.save(item);
```

:::NEW_COMMAND:::
:::UPDATE:::

```dart
await Amplify.DataStore.save(updatedItem);
```

:::NEW_COMMAND:::
:::DELETE:::

```dart
await Amplify.DataStore.delete(toDeleteItem);
```

:::NEW_COMMAND:::
:::QUERY:::

```dart
try {
  List<:::MODEL:::> :::MODEL:::s = await Amplify.DataStore.query(:::MODEL:::.classType);
} catch (e) {
  print("Could not query DataStore: " + e);
}
```
