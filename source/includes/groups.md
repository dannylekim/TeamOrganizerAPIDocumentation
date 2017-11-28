# Groups

## Get all Groups

> Here is the return:

```javascript
[
  {
    _id: "",
    name: "",
    category: "group",
    __v: 1,
    teamLeader: {
      leaderId: "",
      name: ""
    },
    createdDate: "2017-11-27T04:32:21.267Z",
    users: [
      {
        userId: "",
        taskId: []
      },
      {
        userId: "General",
        taskId: [""]
      }
    ]
  }
];
```

<aside class="notice">**This is an Admin route! ** </aside>

Gets all the groups in the database. Requires [Authorization] admin token.

### HTTP Request

`GET http://localhost:4000/groups`

### Returns and Errors

| Code | Message                                      | Description                                                       |
| ---- | -------------------------------------------- | ----------------------------------------------------------------- |
| 200  | Array of Objects                             | Returns all the groups in the database.                           |
| 403  | Access denied. User has no admin privileges. | Token does not possess administrator privileges.                  |
| 401  | Unauthorized                                 | Means that there was no JWT placed into the authorization header. |

## Create Group

> Here is the body of the request: 

```javascript
```

> Here is the return value: 

```javascript
```

Creates the group in the specified user. Requires [Authorization] token. 

### HTTP Request

### Query Parameters 

### Returns and Errors


## Get Group

> Here is the return:

```javascript
  {
    _id: "",
    name: "",
    category: "group",
    __v: 1,
    teamLeader: {
      leaderId: "",
      name: ""
    },
    createdDate: "2017-11-27T04:32:21.267Z",
    users: [
      {
        userId: "",
        taskId: []
      },
      {
        userId: "General",
        taskId: [""]
      }
    ]
  }
```

Gets the specified group. Requires [Authorization] token.

### HTTP Request

`GET http://localhost:4000/:groupId`

### Returns and Errors

| Code | Message                              | Description                         |
| ---- | ------------------------------------ | ----------------------------------- |
| 200  | Group Object                         | Successfully returns a group object |
| 500  | Group does not exist in the database | Group doesn't exist                 |
| 500  | Invalid Cast Object                  | Wrong groupId                       |

## Update Group

> Here is the body of the request: 

```javascript
```

> Here is the return value: 

```javascript
```

Creates the group in the specified user. Requires [Authorization] token. 

### HTTP Request

### Query Parameters 

### Returns and Errors


## Delete Group
