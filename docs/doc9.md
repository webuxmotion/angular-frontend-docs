---
id: doc9
title: Use FormsModule, ReactiveFormsModule
---

1. Edit login-page.component.html
```
<form 
    class="c-form"
    [formGroup]="form"
    (ngSubmit)="onSubmit()"
>
    <div class="card c-form__card">
        <div class="card-content">
            <span class="card-title">Login</span>
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
                [disabled]="form.invalid"
            >Login</button>
        </div>
    </div>
</form>
```

2. Edit login-page.component.ts
```
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
  selector: 'app-login-page',
  templateUrl: './login-page.component.html',
  styleUrls: ['./login-page.component.scss']
})
export class LoginPageComponent implements OnInit {

  form: FormGroup

  constructor() { }

  ngOnInit() {
    this.form = new FormGroup({
      email: new FormControl(null, [Validators.required, Validators.email]),
      password: new FormControl(null, [Validators.required, Validators.minLength(6)])
    })
  }

  onSubmit() {
    
  }

}
```

3. Import modules to app.module.ts
```
import { FormsModule, ReactiveFormsModule } from '@angular/forms';

...
imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule,
    ReactiveFormsModule
],
...
```