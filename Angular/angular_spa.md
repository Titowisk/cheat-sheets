# Angular Single Page Application

## Services
A way to avoid code duplication by using the same functionality across different components

Inside `app/` the `_services/` folder holds services.
Those services can be injected and used across all components of the application.

They can be used in `some.component.ts`:

```
export class AppComponent implements OnInit {
  jwtHelper = new JwtHelperService();

  constructor(private authService: AuthService) {}

  ngOnInit() {
    const token = localStorage.getItem('token');
    if (token) {
      this.authService.decodedToken = this.jwtHelper.decodeToken(token);
    }
  }
}
```

or inside `some.component.html`:

```
<div *ngIf="loggedIn()" class="dropdown">
    <a class="dropdown-toggle text-light">
      Welcome {{authService.decodedToken?.unique_name | titlecase}}
    </a>
  
    <div class="dropdown-menu">
      <a class="dropdown-item" href="#"><i class="fa fa-user"></i>Edit Profile</a>
      <div class="dropdown-divider"></div>
      <a class="dropdown-item" href="#"><i class="fa fa-sign-out"></i>Logout</a>
    </div>
  </div>
```

### Any-to-Any Component Communication

- BehaviorSubject

References:

https://fireship.io/lessons/sharing-data-between-angular-components-four-methods/

## AuthService

## JwtHelper

- Validate token (see if it is expired)
- Decrypt token to get values from it.

## Bootstrap and Angular

https://valor-software.com/ngx-bootstrap/#/

Uses bootstrap and angular but avoids using jquery

## Auth Guard
You can protect routes by only allowing logged users to them.

Look at `routes.ts` and `_guards/` service created using `ng g guard auth --skipTests`


