---
id: doc6
title: Generate components
---

1. Create login page
```
ng g c login-page --spec false
```

2. Create register page
```
ng g c register-page --spec false
```

3. Edit login-page.component.html
```
<form class="c-form">
    <div class="card c-form__card">
        <div class="card-content">
            <span class="card-title">Login</span>
            <div>
                <div class="input-field">
                    <i class="material-icons prefix">account_circle</i>
                    <input id="icon_prefix" type="text" class="validate">
                    <label for="icon_prefix">First Name</label>
                </div>
                <div class="input-field">
                    <i class="material-icons prefix">phone</i>
                    <input id="icon_telephone" type="tel" class="validate">
                    <label for="icon_telephone">Telephone</label>
                </div>
            </div>
        </div>
        <div class="card-action">
            <button class="modal-action waves-effect btn">Login</button>
        </div>
    </div>
</form>
```

4. Edit register-page.component.html
```
<form class="c-form">
    <div class="card c-form__card">
        <div class="card-content">
            <span class="card-title">Create account</span>
            <div>
                <div class="input-field">
                    <i class="material-icons prefix">account_circle</i>
                    <input id="icon_prefix" type="text" class="validate">
                    <label for="icon_prefix">First Name</label>
                </div>
                <div class="input-field">
                    <i class="material-icons prefix">phone</i>
                    <input id="icon_telephone" type="tel" class="validate">
                    <label for="icon_telephone">Telephone</label>
                </div>
            </div>
        </div>
        <div class="card-action">
            <button class="modal-action waves-effect btn">Register</button>
        </div>
    </div>
</form>
```

5. Edit styles.scss
```
@import "~materialize-css/dist/css/materialize.min.css";

.c-form {
    display: flex;
    justify-content: center;
    
    &__card {
        min-width: 500px;
    }
}
```


