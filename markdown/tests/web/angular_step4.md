Add the following polyfills to your `src/polyfills.ts` file to support Angular 6+:
```ts
(window as any).global = window;
(window as any).process = {
  env: { DEBUG: undefined },
};
```

Install the Amplify libraries for your Angular app:
```bash
npm install aws-amplify
```

Configure the Angular app's Amplify instance. Add the following code snippet to the top of your **main.ts**:
```ts
import Amplify from 'aws-amplify'
import awsconfig from './aws-exports'

Amplify.configure(awsconfig)
```