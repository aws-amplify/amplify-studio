:::NEW_COMMAND:::
:::GET_AUTH_SESSION:::
```swift
do {
    let session = try await Amplify.Auth.fetchAuthSession()
    print("Is user signed in: \(session.isSignedIn)")
} catch let error as AuthError {
    print("Fetch auth session failed with error: \(error)")
} catch {
    print("Unexpected error: \(error)")
}
```

:::NEW_COMMAND:::
:::SIGNIN:::
```swift
do {
    let result = try await Amplify.Auth.signIn(
        username: username,
        password: password
    )
    print("Sign in successful: \(result.isSignedIn)")
} catch let error as AuthError {
    print("Sign in failed with error: \(error)")
} catch {
    print("Unexpected error: \(error)")
}
```
:::NEW_COMMAND:::
:::SIGNOUT:::
```swift
let result = await Amplify.Auth.signOut()
guard let signOutResult = result as? AWSCognitoSignOutResult,
        case .complete = signOutResult
else {
    print("Sign out failed to complete")
    return
}
print("Sign out successful")
}
```
:::NEW_COMMAND:::
:::SIGNUP:::
```swift
let userAttributes = [AuthUserAttribute(.email, value: email)]
let options = AuthSignUpRequest.Options(userAttributes: userAttributes)
do {
    let signUpResult = try await Amplify.Auth.signUp(
        username: username,
        password: password,
        options: options
    )
    if case let .confirmUser(deliveryDetails, _, userId) = signUpResult.nextStep {
        print("Delivery details \(String(describing: deliveryDetails)) for userId: \(String(describing: userId)))")
    } else {
        print("SignUp Complete")
    }
} catch let error as AuthError {
    print("An error occurred while registering a user \(error)")
} catch {
    print("Unexpected error: \(error)")
}
```