# Tasks

## Get User's Tasks

> Here is the return value of the get request:

```javascript
[
  {
    _id: "",
    name: "",
    dueDate: null,
    group: "",
    __v: 0,
    category: "Misc.",
    importance: ["urgent"],
    status: ["pending"],
    createdDate: null
  },
  {
    _id: "",
    name: "",
    dueDate: null,
    group: "",
    user: "",
    __v: 0,
    category: "Misc.",
    importance: ["urgent"],
    status: ["pending"],
    createdDate: null
  }
];
```

Gets all user's tasks in every single group that the user is part of. Requires
[Authorization] token.

### HTTP Request

`GET http://localhost:4000/tasks/:userId`

### Returns and Errors

| Code | Message                             | Description                               |
| ---- | ----------------------------------- | ----------------------------------------- |
| 200  | Array of Objects                    | Returns all the tasks that the user has   |
| 200  | User does not have any groups       | User has no groups associated to it       |
| 500  | User does not exist in the database | There is no corresponding user to that ID |
| 500  | Cannot cast Object ID               | userId is incorrect                       |

## Create Task in Group

> Here is an example of the body of the request

```javascript
{
    name: "Name",
    importance: "important",
    dueDate:
    category: "Chores"
    status: "pending"
}
```

> This will return:

```javascript
{
        "_id": "Some Hash",
        "name": "Name",
        "dueDate": null,
        "group": "The Group ID Specified",
        "user": "The user specified",
        "__v": 0,
        "category": "Chores",
        "importance": [
            "important"
        ],
        "status": [
            "pending"
        ],
        "createdDate": null
    }
```

Creates a task inside of the group specified and associated to the user
specified. Requires [Authorization] token.

### HTTP Request

`POST http://localhost:4000/tasks/:groupId/:userId`

### Query Parameters

| Parameter   | Default  | Required | Type   | Description                                                                                            |
| ----------- | -------- | -------- | ------ | ------------------------------------------------------------------------------------------------------ |
| name        |          | true     | String | The name of the task                                                                                   |
| importance  | normal   | false    | String | Importance of the task. Must be one of the three: "normal", "important", "urgent". Default is "normal" |
| dueDate     |          | false    | Date   | The due date of the task                                                                               |
| category    | Misc.    | false    | String | The category of the task                                                                               |
| status      | pending  | false    | String | Status of the task. Must be one of the three: "pending", "ongoing", "completed"                        |
| createdDate | Date.now | true     | Date   | Creation date of the task                                                                              |

### Returns and Errors

| Code | Message                              | Description                                        |
| ---- | ------------------------------------ | -------------------------------------------------- |
| 200  | Task Obj                             | Successfully created the Task                      |
| 200  | There is no such user in the group   | The user in question does not belong in this group |
| 500  | Group does not exist in the database | Invalid group                                      |
| 500  | Invalid Cast Obj                     | Group ID is incorrect                              |

## Get User's Tasks in Group

> Here is the return:

```javascript
[
  {
    _id: "Some Hash",
    name: "",
    dueDate: null,
    group: "",
    user: "",
    __v: 0,
    category: "",
    importance: ["important"],
    status: ["pending"],
    createdDate: null
  }
];
```

Gets all of the specified users tasks inside the specified group. Requires
[Authorization] token. The requester must belong to the group.

### HTTP Request

`GET http://localhost:4000/tasks/:groupId/:userId`

### Returns and Errors

| Code | Message                              | Description                       |
| ---- | ------------------------------------ | --------------------------------- |
| 200  | Array of Objects                     | Successfully return all the tasks |
| 200  | User does not exist                  | User doesn't belong in the group  |
| 500  | Group does not exist in the database | The group doesn't exist           |
| 500  | Invalid Cast Obj                     | GroupId doesn't exist             |

## Update Task

## Delete Task

## Get all Tasks

> Here is the return:

```javascript
[
  {
    _id: "Some Hash",
    name: "",
    dueDate: null,
    group: "",
    user: "",
    __v: 0,
    category: "",
    importance: ["important"],
    status: ["pending"],
    createdDate: null
  }
];
```

<aside class="notice">**This is an Admin route! ** </aside>

Gets all the tasks that belongs to every user in the database. Requires
[Authorization] admin token.

### HTTP Request

`GET http://localhost:4000/tasks`

### Returns and Errors

| Code | Message                                      | Description                                                        |
| ---- | -------------------------------------------- | ------------------------------------------------------------------ |
| 200  | Array of Objects                             | Returns all the tasks in the database.                             |
| 403  | Access denied. User has no admin privileges. | Token does not possess administrator privileges.                   |
| 401  | Unauthorized                                 | Means that there was no JWT placed into the authorization header. |
