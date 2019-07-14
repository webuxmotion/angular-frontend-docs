---
id: doc11
title: Register form
---

1. Edit method register in file /shared/services/auth.service.ts
```
register(user: User): Observable<User> {
  return this.http.post<User>('/api/auth/register', user)
}
```

2. Edit register-page.component.ts
```
import { Component, OnInit, OnDestroy } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';
import { AuthService } from '../shared/services/auth.service';
import { Subscription } from 'rxjs';
import { Router } from '@angular/router';

@Component({
  selector: 'app-register-page',
  templateUrl: './register-page.component.html',
  styleUrls: ['./register-page.component.scss']
})
export class RegisterPageComponent implements OnInit, OnDestroy {

  form: FormGroup
  aSub: Subscription

  constructor(
    private auth: AuthService,
    private router: Router
  ) { }

  ngOnInit() {
    this.form = new FormGroup({
      email: new FormControl(null, [Validators.required, Validators.email]),
      password: new FormControl(null, [Validators.required, Validators.minLength(6)])
    })
  }

  ngOnDestroy() {
    if (this.aSub) {
      this.aSub.unsubscribe()
    }
  }

  onSubmit() {
    this.form.disable()
    this.aSub = this.auth.register(this.form.value).subscribe(
      () => this.router.navigate(['/login'], {
        queryParams: {
          registered: true
        }
      }),
      error => {
        console.warn(error)
        this.form.enable()
      }
    )
  }

}
```

3. Edit register-page.component.html
```
<form 
    class="c-form"
    [formGroup]="form"
    (ngSubmit)="onSubmit()"
>
    <div class="card c-form__card">
        <div class="card-content">
            <span class="card-title">Create account</span>
            <div>
                <div class="input-field">
                    <i class="material-icons prefix">account_circle</i>
                    <input 
                        formControlName="email"
                        type="email" 
                        class="validate"
                        [ngClass]="{'invalid': form.get('email').invalid && form.get('email').touched}"
                    >
                    <label for="icon_prefix">First Name</label>
                    <span 
                        class="helper-text red-text"
                        *ngIf="form.get('email').invalid && form.get('email').touched"
                    >
                        <span *ngIf="form.get('email').errors['required']">Email can't be empty</span>
                        <span *ngIf="form.get('email').errors['email']">Use correct email address</span>
                    </span>
                </div>
                <div class="input-field">
                    <i class="material-icons prefix">phone</i>
                    <input 
                        formControlName="password"
                        type="password"
                        class="validate"
                        [ngClass]="{'invalid': form.get('password').invalid && form.get('password').touched}"
                    >
                    <label for="icon_telephone">Telephone</label>
                    <span 
                        class="helper-text red-text"
                        *ngIf="form.get('password').invalid && form.get('password').touched"
                    >
                        <span *ngIf="form.get('password').errors['required']">Password can't be empty</span>
                        <span *ngIf="form.get('password').errors['minlength'] &&
                            form.get('password').errors['minlength']['requiredLength']">
                            Password should be more than {{form.get('password').errors['minlength']['requiredLength']}} characters.<br>
                            Current count: {{form.get('password').errors['minlength']['actualLength']}}
                        </span>
                    </span>
                </div>
            </div>
        </div>
        <div class="card-action">
            <button 
                type="submit"
                class="modal-action waves-effect btn"
                [disabled]="form.invalid || form.disabled"
            >Register</button>
        </div>
    </div>
</form>
```

4. Create passportless route /register in server. Edit file /routes/auth.js
```
...
//router.post('/register', passport.authenticate('jwt', {session: false}), controller.register)
router.post('/register', controller.register)
```

5. Run server
```
npm run dev
```

6. Try to register on page [http://localhost:4200/register](http://localhost:4200/register)
