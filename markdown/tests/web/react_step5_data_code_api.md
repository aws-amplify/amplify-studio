:::NEW_COMMAND:::
:::CREATE:::

```js
import { API } from "aws-amplify";
import { create:::MODEL::: } from './graphql/mutations';
```

```js
:::NO_COPY:::
...
```

```js
const new:::MODEL::: = await API.graphql({
    query: create:::MODEL:::,
    variables: {
        input: {:::FIELDS:::}
    }
});
```

:::NEW_COMMAND:::
:::UPDATE:::

```js
import { API } from "aws-amplify";
import { update:::MODEL::: } from './graphql/mutations';
```

```js
:::NO_COPY:::
...
```

```js
const updated:::MODEL::: = await API.graphql({
    query: update:::MODEL:::,
    variables: {
        input: {:::FIELDS:::}
    }
});
```

:::NEW_COMMAND:::
:::DELETE:::

```js
import { API } from "aws-amplify";
import { delete:::MODEL::: } from './graphql/mutations';
```

```js
:::NO_COPY:::
...
```

```js
const deleted:::MODEL::: = await API.graphql({
    query: delete:::MODEL:::,
    variables: {
        input: {
            id: "YOUR_RECORD_ID"
        }
    }
});
```

:::NEW_COMMAND:::
:::QUERY:::

```js
import { API } from "aws-amplify";
import { list:::MODEL:::s, get:::MODEL::: } from "./graphql/queries";
```

```js
:::NO_COPY:::
...
```

```js
// List all items
const all:::MODEL:::s = await API.graphql({
    query: list:::MODEL:::s
});
console.log(all:::MODEL:::);
```
```js
// Get a specific item
const one:::MODEL::: = await API.graphql({
    query: get:::MODEL:::,
    variables: { id: 'YOUR_RECORD_ID' }
});
```
