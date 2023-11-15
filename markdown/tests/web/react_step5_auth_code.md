:::NEW_COMMAND:::
:::GET_AUTH_SESSION:::
```js
import { fetchAuthSession } from 'aws-amplify/auth';

async function currentSession() {
  try {
    const { accessToken, idToken } = (await fetchAuthSession()).tokens ?? {};
  } catch (err) {
    console.log(err);
  }
}
```

:::NEW_COMMAND:::
:::SIGNIN:::
```js
import { signIn } from 'aws-amplify/auth';

async function signIn({ username, password }) {
  try {
    const { isSignedIn, nextStep } = await signIn({ username, password });
  } catch (error) {
    console.log('error signing in', error);
  }
}
```
:::NEW_COMMAND:::
:::SIGNOUT:::
```js
import { signOut } from 'aws-amplify/auth';

async function handleSignOut() {
  try {
    await signOut();
  } catch (error) {
    console.log('error signing out: ', error);
  }
}
```
:::NEW_COMMAND:::
:::SIGNUP:::
```js
import { signUp } from 'aws-amplify/auth';

async function handleSignUp({ username, password, email, phone_number }) {
  try {
    const { isSignUpComplete, userId, nextStep } = await signUp({
      username,
      password,
      options: {
        userAttributes: {
          email,
          phone_number // E.164 number convention
        },
        // optional
        autoSignIn: true // or SignInOptions e.g { authFlowType: "USER_SRP_AUTH" }
      }
    });

    console.log(userId);
  } catch (error) {
    console.log('error signing up:', error);
  }
}
```