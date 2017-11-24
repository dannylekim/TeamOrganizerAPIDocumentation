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

> Here is the body of the request 

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

This endpoint authenticates and logs the user into the site. Endpoint returns a token where the payload has both the ID of the user and the privileges the user has. Additionally, the token only lasts for 10 hours before it expires and becomes no longer usable.

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

> Here is the minimum body for the request

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
This endpoint allows a user to be created. The password must not be more than 160 characters and must contain at least 1 of each: numeric, lower case, uppercase and symbol.

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
role | user | false | String | Can either be "admin" or "user" by setting this value to either or.
createdDate | Time of request | false | Date | The date-time of the user's creation 
groups | [  ] | false | Array | Groups that user is part of, default is none. 
notifications | [  ] | false | Array | Notifications that the user has

### Returns and Errors

Code | Message |
----| ------| 
200 | Returns the user object successfully.
200 | Too many characters. Password must not be over 160 characters. 
200 | Password must contain at least a numeric character. 
200 | Password must contain at least a lower case character.
200 | Password must contain at least an upper case character. 
200 | Password must contain at least a symbol character. 
200 | A user with this username already exists, please choose another one. 
200 | This email is already in use!

## Get All Users 

> Returns as follows: 

```javascript
[
  {
        "_id": "5a0bda228918facb5f6",
        "email": "test@mail.com",
        "username": "test",
        "firstName": "test",
        "lastName": "test",
        "password": "$2a$10$G6r06l832j1o2jks0.uXnNwSkFX3nJXS",
        "__v": 0,
        "createdDate": [],
        "notifications": [],
        "groups": [],
        "role": [
            "user"
        ]
    },
      {
        "_id": "5a0aks0gia2wa228918facb5f6",
        "email": "test2@mail.com",
        "username": "test2",
        "firstName": "test2",
        "lastName": "test2",
        "password": "$2a$10$0910285102.uXnNwSkFX3nJXS",
        "__v": 0,
        "createdDate": [],
        "notifications": [],
        "groups": [],
        "role": [
            "admin"
        ]
    },
]
```
<aside class="notice">**This is an Admin route! ** </aside>

Allows the administrator to get all users in the database. Requires [Authorization] header with an admin token.

### HTTP Request

`GET http://localhost:4000/users`

### Returns and Errors 

Code | Message | Description 
-----| ------| ----------|
200 | Array of Objects | Returns all the users in the database. | 
403 | Access denied. User has no admin privileges. | Token does not possess administrator privileges. |
401 | Unauthorized | Means that there was not JWT placed into the authorization header. |


## Delete User 

<aside class="notice">** This is an Admin route! **</aside>

Allows the administrator to remove the user from the database and remove the user from all of his groups and his tasks. 

## Update User Information 

Allows the user to update information about themselves. Specifically: First Name, Last Name and Email 

### HTTP Request 

`PUT http://localhost:4000/users/:userId`

### Returns and Errors

Code | Message | Description
-----| --------| ----------|
200 | Cast to ObjectId failed for value "5a16253bdf50e73c4" at path "_id" for model "User" | There's an incorrect ID




 