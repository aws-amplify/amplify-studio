Pull in the latest backend information into your app's code base. 

1. Open your Terminal, navigate to your project's directory, and run the following command: 
```bash
:::AMPLIFY_PULL_COMMAND:::
```

2. Make sure `Amplify` initialized and configured correctly.
```js
import Amplify from 'aws-amplify'
import awsconfig from './aws-exports'

Amplify.configure(awsconfig)
```