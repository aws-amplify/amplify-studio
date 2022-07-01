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
        input: todoDetails
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
        input: todoDetails
    }
});
```

:::NEW_COMMAND:::
:::QUERY:::

```js
import { API } from "aws-amplify";
import * as queries from "./graphql/queries";
```

```js
:::NO_COPY:::
...
```

```js
// Simple query
const all:::MODEL:::s = await API.graphql({
    query: queries.list:::MODEL:::s
});
console.log(all:::MODEL:::);
// result: { "data": { "list:::MODEL:::s": { "items": [/* ..... */] } } }

// Query using a parameter
const one:::MODEL::: = await API.graphql({
    query: queries.get:::MODEL:::,
    variables: { id: 'some id' }
});
```
