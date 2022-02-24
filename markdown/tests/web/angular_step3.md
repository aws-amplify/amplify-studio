Open an existing Angular project. If you do not have one, use the Angular CLI to create a new project:
```bash
npx -p @angular/cli ng new myapp
```
```bash
:::NO_COPY:::
? Do you want to enforce stricter type checking and stricter bundle budgets in the workspace? N
  This setting helps improve maintainability and catch bugs ahead of time.
  For more information, see https://angular.io/strict 
? Would you like to add Angular routing? Y
? Which stylesheet format would you like to use? (your preferred stylesheet provider)
```
```bash
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

