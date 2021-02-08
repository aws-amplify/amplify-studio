:::NEW_COMMAND:::
:::GET_AUTH_SESSION:::
```java
Amplify.Auth.fetchAuthSession(
    session -> Log.i("AmplifyAuth", "Auth Session: " + session.toString()),
    failure -> Log.e("AmplifyAuth", "Failed to fetch auth session", failure)
);
```

:::NEW_COMMAND:::
:::SIGNIN:::
```java
Amplify.Auth.signIn("username", "password",
    result -> {
        if (result.isSignInComplete()) {
            Log.i("AmplifyAuth", "Sign-in succeeded");
        } else { 
            Log.w("AmplifyAuth", "Sign in not complete");
        }
    },
    failure -> Log.e("AmplifyAuth", "Failed to sign-in.", failure)
);
```
:::NEW_COMMAND:::
:::SIGNOUT:::
```java
Amplify.Auth.signOut(
    () -> Log.i("AmplifyAuth", "Signed out successfully"),
    failure -> Log.e("AmplifyAuth", "Failed to sign out.", failure)
);
```
:::NEW_COMMAND:::
:::SIGNUP:::
```java
Amplify.Auth.signUp("username", "Password123",
    AuthSignUpOptions.builder()
        .userAttribute(AuthUserAttributeKey.email(), "my@email.com")
        .build(),
    result -> Log.i("AmplifyAuth", "Result: " + result.toString()),
    failure -> Log.e("AmplifyAuth", "Sign up failed", failure)
);
```
