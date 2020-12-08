
Install the Amplify libraries for your React app:
```bash
npm install aws-amplify typescript
```

Configure the React app's Amplify instance. Add the following code snippet to the top of your **index.js**:
```js
import Amplify from 'aws-amplify'
import awsconfig from './aws-exports'

Amplify.configure(awsconfig)
```