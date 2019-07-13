---
id: doc10
title: Create auth service
---

1. Create file /shared/services/auth.service.ts with this code
```
import { Injectable } from '@angular/core'
import { HttpClient } from '@angular/common/http'
import { User } from '../interfaces'
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators'


@Injectable({
    providedIn: 'root'
})
export class AuthService {

    private token = null

    constructor(
        private http: HttpClient
    ) {}

    register() {}

    login(user: User): Observable<{token: string}> {
        return this.http.post<{token: string}>('/api/auth/login', user)
            .pipe(
                tap(
                    ({token}) => {
                        localStorage.setItem('auth-token', token)
                        this.setToken(token)
                    }
                )
            )
    }

    setToken(token: string) {
        this.token = token
    }

    getToken(): string {
        return this.token
    }

    isAuthenticated(): boolean {
        return !!this.token
    }

    logout() {
        this.setToken(null)
        localStorage.clear()
    }
}
```

2. Edit login-page.component.ts
```
import { Component, OnInit, OnDestroy } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';
import { AuthService } from '../shared/services/auth.service';
import { Subscription } from 'rxjs';
import { Router, ActivatedRoute, Params } from '@angular/router';

@Component({
  selector: 'app-login-page',
  templateUrl: './login-page.component.html',
  styleUrls: ['./login-page.component.scss']
})
export class LoginPageComponent implements OnInit, OnDestroy {

  form: FormGroup
  aSub: Subscription

  constructor(
    private auth: AuthService,
    private router: Router,
    private route: ActivatedRoute
  ) { }

  ngOnInit() {
    this.form = new FormGroup({
      email: new FormControl(null, [Validators.required, Validators.email]),
      password: new FormControl(null, [Validators.required, Validators.minLength(6)])
    })

    this.route.queryParams.subscribe((params: Params) => {
      if (params['registered']) {
        // now you can login to system 
      } else if (params['accessDenied']) {
        // please authorize
      }
    })
  }

  ngOnDestroy() {
    if (this.aSub) {
      this.aSub.unsubscribe()
    }
  }

  onSubmit() {
    this.form.disable()
    this.aSub = this.auth.login(this.form.value).subscribe(
      () => this.router.navigate(['/overview']),
      error => {
        console.warn(error)
        this.form.enable()
      }
    )
  }

}
```
3. Edit login-page.component.html
```
...
<button 
    type="submit"
    class="modal-action waves-effect btn"
    [disabled]="form.invalid || form.disabled"
>Login</button>
...
```
4. Add HttpClientModule in file app.module.ts
```
import { HttpClientModule } from '@angular/common/http';

...
imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule,
    ReactiveFormsModule,
    HttpClientModule
],
...
```
5. Create file /app/shared/interfaces.ts
```
export interface User {
    email: string,
    password: string
}
```