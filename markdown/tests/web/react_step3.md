Open your existing React project. If you do not have one, create a new React project:

```bash
npx create-react-app@latest myapp
cd myapp
```

Install the Amplify CLI. The Amplify CLI is a command line toolchain that runs locally in order to communicate with your app backend.

```
:::AMPLIFY_INSTALL_COMMAND:::
```

Run the following command from your project's root folder (`myapp`):

```bash
amplify pull --sandboxId :::BACKEND_MANAGER_ID:::
```
