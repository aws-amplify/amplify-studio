Open your existing Vue project. If you do not have one, use the Vue CLI to create a new project:

```bash
npm install -g @vue/cli
```

Once the Vue CLI is installed, create a new Vue project:

```bash
vue create myamplifyproject
```

```bash
:::NO_COPY:::
? Please pick a preset: (Use arrow keys)
❯ default (babel, eslint)   <--
  Manually select features
```

```bash
cd myamplifyproject
```

Install the Amplify CLI. The Amplify CLI is a command line toolchain that runs locally in order to communicate with your app backend.

```
:::AMPLIFY_INSTALL_COMMAND:::
```

Run the following command from your project's root folder (`myamplifyproject`):

```bash
amplify pull --sandboxId :::BACKEND_MANAGER_ID:::
```
