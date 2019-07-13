---
id: doc12
title: Routes protection with guard
---

1. Create folder /app/shared/classes

2. Create file /app/shared/classes/auth.guard.ts and past code:
```
import { CanActivate, CanActivateChild, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router'
import { Observable, of } from 'rxjs';
import { Injectable } from '@angular/core';
import { AuthService } from '../services/auth.service';

@Injectable({
    providedIn: 'root'
})
export class AuthGuard implements CanActivate, CanActivateChild {

    constructor(
        private auth: AuthService,
        private router: Router
    ) {}

    canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<boolean> {
        if (this.auth.isAuthenticated()) {
            return of(true)
        } else {
            this.router.navigate(['/login'], {
                queryParams: {
                    accessDenied: true
                }
            })
            return of(false)
        }
    }

    canActivateChild(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<boolean> {
        return this.canActivate(route, state)
    }
}
```

3. Use guard for router "register" in file app-routing.module.ts
```
import { AuthGuard } from './shared/classes/auth.guard';

...
{ path: 'register', component: RegisterPageComponent, canActivate: [AuthGuard] }
...
```

4. Run server
```
npm run dev
```

5. Try to see the page [http://localhost:4200/register](http://localhost:4200/register)