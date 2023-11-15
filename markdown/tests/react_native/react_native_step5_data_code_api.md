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
        input: todoDetails
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
        input: todoDetails
    }
});
```

:::NEW_COMMAND:::
:::QUERY:::

```js
import { generateClient } from "aws-amplify/api";
import * as queries from "./graphql/queries";

const client = generateClient()
```

```js
:::NO_COPY:::
...
```

```js
// Simple query
const all:::MODEL:::s = await client.graphql({
    query: queries.list:::MODEL:::s
});
console.log(all:::MODEL:::);
// result: { "data": { "list:::MODEL:::s": { "items": [/* ..... */] } } }

// Query using a parameter
const one:::MODEL::: = await client.graphql({
    query: queries.get:::MODEL:::,
    variables: { id: 'some id' }
});
```
