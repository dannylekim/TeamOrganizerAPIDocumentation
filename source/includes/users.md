# Users

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

This endpoint allows a user to be created. The password must not be more than
160 characters and must contain at least 1 of each: numeric, lower case,
uppercase and symbol.

### HTTP Request

`POST http://localhost:4000/signup`

### Query Parameters

| Parameter     | Default         | Required | Type   | Description                                                         |
| ------------- | --------------- | -------- | ------ | ------------------------------------------------------------------- |
| email         |                 | true     | String | The email that the user wants to sign up with                       |
| username      |                 | true     | String | The username that the user wants to sign up with                    |
| firstName     |                 | true     | String | User's first name                                                   |
| lastName      |                 | true     | String | User's last name                                                    |
| password      |                 | true     | String | User's inputted password. Password will be salted and hashed.       |
| role          | user            | false    | String | Can either be "admin" or "user" by setting this value to either or. |
| createdDate   | Time of request | false    | Date   | The date-time of the user's creation                                |
| groups        | [ ]             | false    | Array  | Groups that user is part of, default is none.                       |
| notifications | [ ]             | false    | Array  | Notifications that the user has                                     |

### Returns and Errors

| Code | Message                                                              | Description                 |
| ---- | -------------------------------------------------------------------- | --------------------------- |
| 200  | Returns the user object successfully.                                | The request was successful. |
| 200  | Too many characters. Password must not be over 160 characters.       |
| 200  | Password must contain at least a numeric character.                  |
| 200  | Password must contain at least a lower case character.               |
| 200  | Password must contain at least an upper case character.              |
| 200  | Password must contain at least a symbol character.                   |
| 200  | A user with this username already exists, please choose another one. |
| 200  | This email is already in use!                                        |

## Get All Users

> Returns as follows:

```javascript
[
  {
    _id: "5a0bda228918facb5f6",
    email: "test@mail.com",
    username: "test",
    firstName: "test",
    lastName: "test",
    password: "$2a$10$G6r06l832j1o2jks0.uXnNwSkFX3nJXS",
    __v: 0,
    createdDate: [],
    notifications: [],
    groups: [],
    role: ["user"]
  },
  {
    _id: "5a0aks0gia2wa228918facb5f6",
    email: "test2@mail.com",
    username: "test2",
    firstName: "test2",
    lastName: "test2",
    password: "$2a$10$0910285102.uXnNwSkFX3nJXS",
    __v: 0,
    createdDate: [],
    notifications: [],
    groups: [],
    role: ["admin"]
  }
];
```

<aside class="notice">**This is an Admin route! ** </aside>

Allows the administrator to get all users in the database. Requires
[Authorization] header with an admin token.

### HTTP Request

`GET http://localhost:4000/users`

### Returns and Errors

| Code | Message                                      | Description                                                        |
| ---- | -------------------------------------------- | ------------------------------------------------------------------ |
| 200  | Array of Objects                             | Returns all the users in the database.                             |
| 403  | Access denied. User has no admin privileges. | Token does not possess administrator privileges.                   |
| 401  | Unauthorized                                 | Means that there was no JWT placed into the authorization header. |

## Delete User

<aside class="notice">** This is an Admin route! **</aside>

Allows the administrator to remove the user from the database and remove the
user from all of his groups and his tasks. Requires [Authorization] header with
an admin token.

## Update User Information

Allows the user to update information about themselves. Specifically: First
Name, Last Name and Email. Requires the [Authorization] header with a token.

### HTTP Request

> Here is an example request body, you need only 1 field to have a valid
> request.

```javascript
{
  firstName: "Team",
  lastName: "Organizer",
  email: "teamOrganizer@mail.com"
}
```

> Here is the return value:

```javascript
{
  message: "Successfully updated the user's information.";
}
```

`PUT http://localhost:4000/users/:userId`

### Query Parameters

| Parameter | Default | Required | Type   | Description                     |
| --------- | ------- | -------- | ------ | ------------------------------- |
| firstName |         | false    | String | The new first name of the user. |
| lastName  |         | false    | String | The new last name of the user.  |
| email     |         | false    | String | The new email of the user.      |

### Returns and Errors

| Code | Message                                                             | Description                             |
| ---- | ------------------------------------------------------------------- | --------------------------------------- |
| 200  | Successfully updated the user's information.                        | Succesful request and updated the user. |
| 200  | Cast to ObjectId failed for value "" at path "_id" for model "User" | There's an incorrect ID in the userId   |
| 200  | You need to change at least one thing!                              | User has an empty body for a request.   |

<aside class="warning"> Remember that you need to have at least 1 parameter to consider this a valid request! </aside>

## Change User Password

Allows the user to change their password to another one. Requires an
[Authorization] header with a token.

> Here is how the body of request would look like

```javascript
{
  password: "newPassword";
}
```

> Here is what the return of the request would be:

```javascript
{
  message: "Password has successfully been changed";
}
```

### HTTP Request

`PUT localhost:4000/changePassword/:userId`

### Query Parameters

| Parameter | Default | Required | Type   | Description                   |
| --------- | ------- | -------- | ------ | ----------------------------- |
| password  |         | true     | String | The new password for the user |

### Returns and errors

| Code | Message                                                             | Description                                                  |
| ---- | ------------------------------------------------------------------- | ------------------------------------------------------------ |
| 200  | Password has successfully been changed                              | The request has been accepted and password has been changed. |
| 200  | Please input a password                                             | Empty body request                                           |
| 200  | Please input a new password                                         | The password is the same as the previous                     |
| 200  | Cast to ObjectId failed for value "" at path "_id" for model "User" | Sent an incorrect ID as the userId                           |
