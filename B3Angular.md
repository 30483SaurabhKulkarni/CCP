### Angular

Install Angular In Your Machine Globally

```shell
npm install -g @angular/cli
```

Create new Angular Project
```
ng new my-project
```

- Fill up required information
- Yes for CSS

If required (Optional)
```
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

After created, need to go to project directory
```
cd my-project
```

Add bootstrap in index.html
``` HTML
<!-- Bootstrap Style -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">

<!-- Bootstrap JavaScript Liabrary -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
```

To create a **User Component**
```
ng g component user
```

</br>
</br>

Go to user.component.index.html
``` HTML
<div class="container">
    <!-- jsutify content -->
    <div class="mb-3 row">
        <div class="col-12">
            <div class="row justify-content-around">
                <div class="col-4">
                    <label for="username" class="form-label">Username</label>
                    <input type="text" class="form-control" id="username"
                           [(ngModel)]="username">
                </div>
                <div class="col-4">
                    <label for="password" class="form-label">Password</label>
                    <input type="password" class="form-control" id="password"
                           [(ngModel)]="password">
                </div>
                <div class="row justify-content-around mt-3">
                    <div class="col-2 mt-3">
                        <button class="btn btn-primary" (click)="AddData()">Add
                            User</button>
                    </div>
                    <div class="col-2 mt-3">
                        <button class="btn btn-danger" (click)="userList.pop()">Delete
                            User</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- </form> -->
    <hr />
    <div class="container mt-3 bg-success text-white p-2 rounded
position-absolute">
        <!-- <ul class="list-group list-group-horizontal"> -->
        <ul class="row justify-content-around text-dark text-center p-2 rounded
position-relative">
            <h5 class="col-3">Sr. No</h5>
            <h5 class="col-3">Usernames</h5>
            <h5 class="col-3">Passwords</h5>
        </ul>
        <div *ngFor="let user of userList; index as indexOfelement;">
            <ul class="row justify-content-around p-2 text-center">
                <span class="col-3">{{indexOfelement}}</span>
                <span class="col-3">{{user.name}}</span>
                <span class="col-3">{{user.pass}}</span>
            </ul>
        </div>
    </div>
    <!-- </ol> -->
</div>

```

Go to user.component.ts
``` ts
import {Component, OnInit} from '@angular/core';
import {FormsModule} from "@angular/forms";
import {NgForOf} from "@angular/common";
@Component({
    selector: 'app-user',
    standalone: true,
    imports: [
        FormsModule,
        NgForOf
    ],
    templateUrl: './user.component.html',
    styleUrl: './user.component.css'
})
export class UserComponent implements OnInit {
    username = '';
    password = '';
    userList = [{
        name: "Shivendra",
        pass: "123"
    },
        {
            name: "Shiv",
            pass: "345"
        }];
    AddData = () => {
        console.log("clicked");
        let temp = {name: this.username, pass: this.password}
        this.userList.push(temp);
    }
    constructor() {
    }
    ngOnInit(): void {
    }
}
```

Go to app.component.ts,
Replace with below code
``` ts
<p class="text-white bg-dark p-3">User Dashboard</p>
<app-user></app-user>
```


After running this below command, you get link of localhost://4200
```
ng serve
```
