# Authentication

```javascript
"Welcome to Team Organizer API! Let's get started";
```

Team Organizer uses JSON Web Tokens as a means to pass from request to request
with passport as the middleware. In this manner, you're able to have a secure
method into all API Routes. Therefore, Team Organizer expects this to be in all
your Authorization headesr

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

This endpoint authenticates and logs the user into the site. Endpoint returns a
token where the payload has both the ID of the user and the privileges the user
has. Additionally, the token only lasts for 10 hours before it expires and
becomes no longer usable.

### HTTP Request

`POST http://localhost:4000/login`

### Query Parameters

| Parameter | Type   | Description         |
| --------- | ------ | ------------------- |
| username  | String | The user's username |
| password  | String | The user's password |

### Returns and Errors

| Code | Message                           | Description                          |
| ---- | --------------------------------- | ------------------------------------ |
| 200  | Login Successful                  | Successfully logged in.              |
| 401  | Please input a username           | Occurs when empty username field.    |
| 401  | Please input a password           | Occurs when empty password field.    |
| 401  | User has not been found           | User does not exist in the database. |
| 401  | Wrong Password. Please try again. | Inputted the wrong password.         |