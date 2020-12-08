Amplify DataStore allows you to manage your app data without writing additional code for offline and online scenarios.

For demonstration purposes, let's set up the content within `app.component.ts`'s `onInit` handler.

```ts
import { Component, OnInit } from '@angular/core';
```
```ts
:::NO_COPY:::
...
export class AppComponent implements OnInit {
  title = 'myamplifyapp';
```
```ts
  async ngOnInit() {
    // ... Place DataStore in here
  }
```
```ts
:::NO_COPY:::
}
```