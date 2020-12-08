:::NEW_COMMAND:::
:::GET_AUTH_SESSION:::
```java
Amplify.Auth.fetchAuthSession(
        result -> Log.i("Amplify Auth", result.toString()),
        error -> Log.e("Amplify Auth", error.toString())
);
```

:::NEW_COMMAND:::
:::SIGNIN:::
```java
Amplify.Auth.signIn(
    "username",
    "password",
    result -> Log.i("Amplify Auth", result.isSignInComplete() ? "Sign in succeeded" : "Sign in not complete"),
    error -> Log.e("Amplify Auth", error.toString())
);
```
:::NEW_COMMAND:::
:::SIGNOUT:::
```java
Amplify.Auth.signOut(
    () -> Log.i("Amplify Auth", "Signed out successfully"),
    error -> Log.e("Amplify Auth", error.toString())
);
```
:::NEW_COMMAND:::
:::SIGNUP:::
```java
Amplify.Auth.signUp(
        "username",
        "Password123",
        AuthSignUpOptions.builder().userAttribute(AuthUserAttributeKey.email(), "my@email.com").build(),
        result -> Log.i("Amplify Auth", "Result: " + result.toString()),
        error -> Log.e("Amplify Auth", "Sign up failed", error)
);
```