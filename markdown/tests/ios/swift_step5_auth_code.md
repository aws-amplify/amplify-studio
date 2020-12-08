:::NEW_COMMAND:::
:::GET_AUTH_SESSION:::
```swift
_ = Amplify.Auth.fetchAuthSession { result in
    switch result {
    case .success(let session):
        print("Is user signed in - \(session.isSignedIn)")
    case .failure(let error):
        print("Fetch session failed with error \(error)")
    }
}
```

:::NEW_COMMAND:::
:::SIGNIN:::
```swift
Amplify.Auth.signIn(username: username, password: password) { result in
    switch result {
    case .success:
        print("Sign in succeeded")
    case .failure(let error):
        print("Sign in failed \(error)")
    }
}
```
:::NEW_COMMAND:::
:::SIGNOUT:::
```swift
Amplify.Auth.signOut() { result in
    switch result {
    case .success:
        print("Successfully signed out")
    case .failure(let error):
        print("Sign out failed with error \(error)")
    }
}
```
:::NEW_COMMAND:::
:::SIGNUP:::
```swift
let userAttributes = [AuthUserAttribute(.email, value: email)]
let options = AuthSignUpRequest.Options(userAttributes: userAttributes)
Amplify.Auth.signUp(username: username, password: password, options: options) { result in
    switch result {
    case .success(let signUpResult):
        if case let .confirmUser(deliveryDetails, _) = signUpResult.nextStep {
            print("Delivery details \(String(describing: deliveryDetails))")
        } else {
            print("SignUp Complete")
        }
    case .failure(let error):
        print("An error occurred while registering a user \(error)")
    }
}
```