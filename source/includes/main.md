# Introduction

Welcome to Team Organizer's API Reference. Here you can find the API references for the service to use if you're a developer wanting to use our API calls. 

We only have language bindings for javascript at the moment which will be on the tabs to the right as you scroll down the documentation.

# Authentication

Team Organizer uses JSON Web Tokens as a means to pass from request to request with passport as the middleware. In this manner, you're able to have a secure method into all API Routes. Therefore, Team Organizer expects this to be in all your Authorization headesr

`Authorization: Bearer Token`

<aside class="notice">
You must replace <code>Token </code> with token gained from logging in.
</aside>

## Login

```json
{
  username: "Username",
  password: "Password"
}

``` 

> the above command returns a JSON structured like so: 

```json
{
  message: "Login Successful",
  token: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVhMDhhZjQ4NDBiNDI5MjQ4Y2Q0YzQ2ZSIsImlhdCI6MTUxMDUyMDE2OH0.WFydp-dRHJiw3532rveMTNp9bxas9kMIDB81M5o5hfs"
}
```

## Get All Kittens


```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```bash
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve
