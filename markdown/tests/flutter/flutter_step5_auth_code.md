:::NEW_COMMAND:::
:::GET_AUTH_SESSION:::

```dart
try {
  CognitoAuthSession res = await Amplify.Auth.fetchAuthSession(
    options: CognitoSessionOptions(getAWSCredentials: true)
  );
} on AuthError catch (e) {
  print(e);
}
```

:::NEW_COMMAND:::
:::SIGNIN:::

```dart
try {
  SignInResult res = await Amplify.Auth.signIn(
    username: usernameController.text.trim(),
    password: passwordController.text.trim(),
  );
  setState(() {
    isSignedIn = res.isSignedIn;
  });
} on AuthError catch (e) {
  print(e);
}
```

:::NEW_COMMAND:::
:::SIGNOUT:::

```dart
try {
  Amplify.Auth.signOut()
} on AuthError catch (e) {
  print(e);
}
```

:::NEW_COMMAND:::
:::SIGNUP:::

```dart
try {
  Map<String, dynamic> userAttributes = {
    "email": emailController.text,
    "phone_number": phoneController.text,
    // additional attributes as needed
  };
  SignUpResult res = await Amplify.Auth.signUp(
    username: "myusername",
    password: "mysupersecurepassword",
    options: CognitoSignUpOptions(
      userAttributes: userAttributes
    )
  );
  setState(() {
    isSignUpComplete = res.isSignUpComplete;
  });
} on AuthError catch (e) {
  print(e);
}
```
