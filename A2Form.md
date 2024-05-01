To create a form based 

Insert in index.html
``` html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Assignment 1B</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.1/dist/css/bootstrap.min.css"
          integrity="sha384-zCbKRCUGaJDkqS1kPbPd7TveP5iyJE0EjAuZQTgFLD2ylzuqKfdKlfG/eSrtxUkn" crossorigin="anonymous">
</head>

<body>
<div class="container">
    <button class="btn btn-outline-success mt-5" data-toggle="modal" data-target="#addNewUser">Add New
        Entry</button>
    <table class="table table-dark my-5 table-striped table-hover rounded-lg">
        <thead>
        <tr>
            <th scope="col">#</th>
            <th scope="col">Name</th>
            <th scope="col">Username</th>
            <th scope="col">Email</th>
            <th scope="col">Phone</th>
            <th scope="col">City</th>
            <th scope="col">Website</th>
        </tr>
        </thead>
        <tbody id="tbody">
        </tbody>
    </table>

    <div class="modal fade" id="addNewUser">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <form>
                        <div class="form-group">
                            <label for="email">Email address</label>
                            <input type="email" class="form-control" id="email">
                        </div>
                        <div class="form-group">
                            <label for="text">Name</label>
                            <input type="text" class="form-control" id="name">
                        </div>
                        <div class="form-group">
                            <label for="text">Username</label>
                            <input type="text" class="form-control" id="username">
                        </div>
                        <div class="form-group">
                            <label for="text">City</label>
                            <input type="text" class="form-control" id="city">
                        </div>
                        <div class="form-group">
                            <label for="text">website</label>
                            <input type="text" class="form-control" id="website">
                        </div>
                        <div class="form-group">
                            <label for="text">phone</label>
                            <input type="text" class="form-control" id="phone">
                        </div>
                        <div class="form-group">
                            <label for="password">Password</label>
                            <input type="password" class="form-control" id="password">
                        </div>
                        <button type="submit" id="btn" data-dismiss="modal" class="btn btn-primary">Submit</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</div>



<script src="./main.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.slim.min.js"
        integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj"
        crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js"
        integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN"
        crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.1/dist/js/bootstrap.min.js"
        integrity="sha384-VHvPCCyXqtD5DqJeNxl2dtTyhF78xXNXdkwX1CZeRusQfRKp+tA7hAShOK/B/fQ2"
        crossorigin="anonymous"></script>
</body>

</html>
```


main.js
``` js
let fetchData = () => {
    let httprequest = new XMLHttpRequest()
    httprequest.open("GET", "https://jsonplaceholder.typicode.com/users/")
    httprequest.send()
    httprequest.onload = () => {
        let res = JSON.parse(httprequest.responseText)
        console.log(res)
        localStorage.setItem("users", JSON.stringify(res))
        displayData()
    }
}

let displayData = () => {
    let tbody = document.getElementById("tbody")
    tbody.innerHTML = ""
    let storedUser = JSON.parse(localStorage.getItem("users"))
    storedUser.map((user , index) => (
        tbody.innerHTML += `
                <tr>
                    <td>${index+1}</td>
                    <td>${user.name}</td>
                    <td>${user.username}</td>
                    <td>${user.email}</td>
                    <td>${user.phone}</td>
                    <td>${user.address.city}</td>
                    <td>${user.website}</td>
                </tr>`
    ))
}
//initial Data
fetchData()

let btn = document.getElementById("btn")
btn.addEventListener("click", () => {
    const email = document.getElementById("email").value
    const username = document.getElementById("username").value
    const password = document.getElementById("password").value
    const name = document.getElementById("name").value
    const city = document.getElementById("city").value
    const website = document.getElementById("website").value
    const phone = document.getElementById("phone").value

    let postObject = {
        email, password, name, website, phone ,username,  address:{
            city:city
        }
    }

    let xhr = new XMLHttpRequest()
    xhr.open("POST", "https://jsonplaceholder.typicode.com/users/")
    xhr.setRequestHeader('Content-type', 'application/json; charset=UTF-8')
    xhr.send(JSON.stringify(postObject))

    xhr.onload = () => {
        if (xhr.status == 201) {
            // let res = xhr.response
            // console.log(res)
            let storedUser = JSON.parse(localStorage.getItem("users"))
            storedUser.unshift(postObject)
            localStorage.setItem("users", JSON.stringify(storedUser))
            displayData()
        }
    }
})
```

data.json
``` json
[
  {
    "name":"Gaurav Shinde",
    "username":"gauravshinde1816",
    "email":"gauravshinde@gmail.com",
    "password":"12345",
    "college":"pict"
  },
  {
    "name":"Saurabh Shinde",
    "username":"saurabhshinde1816",
    "email":"saurabhshinde@gmail.com",
    "password":"12345",
    "college":"pict"
  }
]
```
