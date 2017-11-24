# Authentication

```javascript

"Welcome to Team Organizer API! Let's get started"
```

Team Organizer uses JSON Web Tokens as a means to pass from request to request with passport as the middleware. In this manner, you're able to have a secure method into all API Routes. Therefore, Team Organizer expects this to be in all your Authorization headesr

`Authorization: Bearer Token`

<aside class="notice">
You must replace <code>Token </code> with token gained from logging in.
</aside>

## Login

```javascript
{
  username: "Username",
  password: "Password"
}

``` 

> On succesful login, the return is as follows:

```javascript
{
  message: "Login Successful",
  token: "Bearer [Token]"
}
```

> where [Token] is the hashed JWT
This endpoint authenticates and logs the user into the site. 

### HTTP Request

`POST http://localhost:4000/login`

### Query Parameters

Parameter | Type|  Description
----------| ----| -----------
username | String | The user's username
password | String | The user's password

### Returns and Errors

Code | Message | Description
-----| --------| ------
200 | Login Successful | Successfully logged in.
401 |  Please input a username | Occurs when empty username field.
401 | Please input a password | Occurs when empty password field.
401 | User has not been found | User does not exist in the database.
401 | Wrong Password. Please try again. | Inputted the wrong password.


# User APIs

## Sign up 

```javascript
{
  email:
  username: 
  firstName:
  lastName:
  password: 
}
```

> On succesful user creation, the return is as follows: 

```javascript
{
    "__v": 0,
    "email": "test@mail.com",
    "username": "test",
    "firstName": "test",
    "lastName": "test",
    "_id": "5a176fc7419f4239cc8a0ae6",
    "createdDate": [],
    "notifications": [],
    "groups": []
}
```
This endpoint allows a user to be created. 

### HTTP Request

`POST http://localhost:4000/signup`

### Query Parameters

Parameter | Default | Required | Type | Description 
---------| ---------| --------| ---------| --------|
email | | true | String | The email that the user wants to sign up with
username | | true | String | The username that the user wants to sign up with 
firstName | | true | String | User's first name
lastName | | true | String | User's last name
password | | true | String | User's inputted password. Password will be salted and hashed. 
role | user | false | String | Can either be "admin" or "user"
createdDate | Time of request | false | Date | The date-time of the user's creation 
groups | [  ] | false | Array | Groups that user is part of
notifications | [  ] | false | Array | Notifications that the user has

### Returns and Errors



