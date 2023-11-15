:::NEW_COMMAND:::
:::CREATE:::

```js
import { generateClient } from "aws-amplify/api";
import { create:::MODEL::: } from './graphql/mutations';

const client = generateClient()
```

```js
:::NO_COPY:::
...
```

```js
const new:::MODEL::: = await client.graphql({
    query: create:::MODEL:::,
    variables: {
        input: {:::FIELDS:::}
    }
});
```

:::NEW_COMMAND:::
:::UPDATE:::

```js
import { generateClient } from "aws-amplify/api";
import { update:::MODEL::: } from './graphql/mutations';

const client = generateClient()
```

```js
:::NO_COPY:::
...
```

```js
const updated:::MODEL::: = await client.graphql({
    query: update:::MODEL:::,
    variables: {
        input: {:::FIELDS:::}
    }
});
```

:::NEW_COMMAND:::
:::DELETE:::

```js
import { generateClient } from "aws-amplify/api";
import { delete:::MODEL::: } from './graphql/mutations';

const client = generateClient()
```

```js
:::NO_COPY:::
...
```

```js
const deleted:::MODEL::: = await client.graphql({
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
import { generateClient } from "aws-amplify/api";
import { list:::MODEL:::s, get:::MODEL::: } from "./graphql/queries";

const client = generateClient()
```

```js
:::NO_COPY:::
...
```

```js
// List all items
const all:::MODEL:::s = await client.graphql({
    query: list:::MODEL:::s
});
console.log(all:::MODEL:::);
```
```js
// Get a specific item
const one:::MODEL::: = await client.graphql({
    query: get:::MODEL:::,
    variables: { id: 'YOUR_RECORD_ID' }
});
```
