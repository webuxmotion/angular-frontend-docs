---
id: doc14
title: MaterialService and toast
---

1. Create file /classes/material.service.ts
```
declare var M

export class MaterialService {

    static toast(message: string) {
        M.toast({ html: message })
    }
}
```

2. Use MaterialService in ngOnInit() and onSubmit() methods in file login-page.component.ts
```
import { MaterialService } from '../shared/classes/material.service';

ngOnInit() {
  this.form = new FormGroup({
    email: new FormControl(null, [Validators.required, Validators.email]),
    password: new FormControl(null, [Validators.required, Validators.minLength(6)])
  })

  this.route.queryParams.subscribe((params: Params) => {
    if (params['registered']) {
      MaterialService.toast('now you can login to system')
    } else if (params['accessDenied']) {
      MaterialService.toast('please authorize')
    } else if (params['sessionFailed']) {
      MaterialService.toast('Please login again')
    }
  })
}

onSubmit() {
    this.form.disable()
    this.aSub = this.auth.login(this.form.value).subscribe(
      () => this.router.navigate(['/overview']),
      error => {
        MaterialService.toast(error.error.message)
        this.form.enable()
      }
    )
  }
```
3. Use MaterialService in onSubmit() method in file register-page.component.ts
```
import { MaterialService } from '../shared/classes/material.service';

onSubmit() {
    this.form.disable()
    this.aSub = this.auth.register(this.form.value).subscribe(
      () => this.router.navigate(['/login'], {
        queryParams: {
          registered: true
        }
      }),
      error => {
        MaterialService.toast(error.error.message)
        this.form.enable()
      }
    )
  }
```