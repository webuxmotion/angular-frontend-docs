---
id: doc7
title: Setup routing
---

1. If you don't have file /client/src/app/app-routing.module.ts, create it:
```typescript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';


const routes: Routes = [];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

2. After file creating, add AppRoutingModule in file app.module.ts
```
import { AppRoutingModule } from './app-routing.module';

...
imports: [
    BrowserModule,
    AppRoutingModule
],
...
```

3. Edit file app-routing.module.ts
```
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { LoginPageComponent } from './login-page/login-page.component';
import { RegisterPageComponent } from './register-page/register-page.component';


const routes: Routes = [
  {path: 'login', component: LoginPageComponent},
  { path: 'register', component: RegisterPageComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

4. Edit file app.component.html
```
<h1>Working</h1>
<router-outlet></router-outlet>
```

5. Check route in browser [http://localhost:4200/login](http://localhost:4200/login)