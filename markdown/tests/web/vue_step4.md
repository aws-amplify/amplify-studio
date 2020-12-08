
Install the Amplify libraries for your Vue app:
```bash
yarn add aws-amplify
```

Configure the Vue app's Amplify instance. Add the following code snippet to the top of your **main.js**:
```js
import Amplify from 'aws-amplify'
import awsconfig from './aws-exports'

Amplify.configure(awsconfig)
```