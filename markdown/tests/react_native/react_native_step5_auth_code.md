:::NEW_COMMAND:::
:::GET_AUTH_SESSION:::
```js
Auth.currentSession()
  .then(data => console.log(data))
  .catch(err => console.log(err));
```

:::NEW_COMMAND:::
:::SIGNIN:::
```js
try {
    const user = await Auth.signIn(username, password);
} catch (error) {
    console.log('error signing in', error);
}
```
:::NEW_COMMAND:::
:::SIGNOUT:::
```js
try {
    await Auth.signOut();
} catch (error) {
    console.log('error signing out: ', error);
}
```
:::NEW_COMMAND:::
:::SIGNUP:::
```js
try {
    const { user } = await Auth.signUp({ username, password });
    console.log(user);
} catch (error) {
    console.log('error signing up:', error);
}
```