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

## Bootstrap and Angular
https://valor-software.com/ngx-bootstrap/#/

Uses bootstrap and angular but avoids using jquery