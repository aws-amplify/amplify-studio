:::NEW_COMMAND:::
:::GET_AUTH_SESSION:::
```kotlin
Amplify.Auth.fetchAuthSession(
    { Log.i("AmplifyAuth", "Session: $it") },
    { Log.e("AmplifyAuth", "Failed to fetch session" it) }
)
```

:::NEW_COMMAND:::
:::SIGNIN:::
```kotlin
Amplify.Auth.signIn("username", "password",
    {
        if (result.isSignInComplete()) {
            Log.i("AmplifyAuth", "Sign in succeeded")
        } else {
            Log.w("AmplifyAuth", "Sign in not complete")
        }
    },
    { Log.e("AmplifyAuth", "Sign in failed", it) }
)
```
:::NEW_COMMAND:::
:::SIGNOUT:::
```kotlin
Amplify.Auth.signOut(
    { Log.i("AmplifyAuth", "Signed out successfully") },
    { Log.e("AmplifyAuth", "Failed to sign out", it) }
)
```
:::NEW_COMMAND:::
:::SIGNUP:::
```kotlin
Amplify.Auth.signUp("username", "Password123",
    AuthSignUpOptions.builder()
        .userAttribute(AuthUserAttributeKey.email(), "my@email.com")
        .build(),
    { Log.i("AmplifyAuth", "Result: $it") },
    { Log.e("AmplifyAuth", "Sign up failed", it) }
)
```
