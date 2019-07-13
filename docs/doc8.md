---
id: doc8
title: Create layout
---

1. Generate layout
```
ng g c shared/layouts/auth-layout --spec false
```
2. Edit auth-layout.component.html
```
<nav>
    <div class="nav-wrapper">
        <a  routerLink="/" class="brand-logo">Logo</a>
        <ul class="right hide-on-med-and-down">
            <li routerLinkActive="active">
                <a routerLink="/login">Login</a>
            </li>
            <li routerLinkActive="active">
                <a routerLink="/register">Register</a>
            </li>
        </ul>
    </div>
</nav>
<div class="auth-layout__content">
    <router-outlet></router-outlet>
</div>
```
3. Edit auth-layout.component.scss
```
.auth-layout {
    
    &__content {
        padding-top: 50px;
    }
}
```
4. Add layout to routes in file app-routing.module.ts
```
import { AuthLayoutComponent } from './shared/layouts/auth-layout/auth-layout.component';

const routes: Routes = [
  {
      path: '', component: AuthLayoutComponent, children: [
          { path: '', redirectTo: "/login", pathMatch: 'full' },
          { path: 'login', component: LoginPageComponent },
          { path: 'register', component: RegisterPageComponent }
      ]
  }
];
```

5. Edit file app.component.html
```
<router-outlet></router-outlet>
```