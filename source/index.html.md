---
title: WYE API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the WYE API! You can use our API to access WYE API endpoints, which can get information related to escape games.

We have language bindings in Python and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

WYE currently uses cookies for authentication.

The server will setup the correct <code>sessionid</code> cookie as soon as you log in through the API, that you then need to pass to any further call.

While cookies are not ideal when dealing with APIs, as they are limited by cross-domain restrictions or may be a bit more difficult to setup in non-browser environment, they were by far the fastest to setup for this first API version.

# GraphQL powered

There is only one endpoint currently available through the API:

`https://real-wye-api.com/graphql/`

| action name | type     | HTTP method | Description |
| ----------- | -------- | ----------- | ----------- |
| createUser  | mutation | POST        | Create user |
| loginUser   | mutation | POST        | Log user in |

## createUser

> To create a new user, use this GraphQL query (`POST` method):

```javascript
mutation {
  createUser(email: "romain@wye.com", pseudo: "Romain", password: "pass") {
    user {
      email,
      pseudo
    }
  }
}
```

> Expected response:

```json
{
  "data": {
    "createUser": {
      "user": {
        "email": "romain@wye.com",
        "pseudo": "Romain"
      }
    }
  }
}
```

The first thing to do is to create an account for a new user.

| Parameter | Mandatory | Description                                             |
| --------- | --------- | ------------------------------------------------------- |
| email     | Yes       | Email of the user, will be used for login               |
| pseudo    | Yes       | Used to identify a user on public pages (rankings, etc) |
| password  | YES       | Password needed for login                               |

## loginUser

> To login as a user, use this GraphQL query (`POST` method):

```javascript
mutation {
  loginUser(email: "romain@wye.com", password: "pass") {
    user {
      email,
      pseudo
    }
  }
}
```

> Expected response:

```json
{
  "data": {
    "loginUser": {
      "user": {
        "email": "romain@wye.com",
        "pseudo": "Romain"
      }
    }
  }
}
```

After creating a new user, the next step is to log in using the same credentials as the user creation.

This mutation will return a <code>sessionid</code> cookie.

<aside class="notice">This cookie should be sent back to the server on each query/mutation other than user creation and user login.</aside>

| Parameter | Mandatory | Description                                 |
| --------- | --------- | ------------------------------------------- |
| email     | Yes       | Email of the user provided on user creation |
| password  | Yes       | Password provided on user creation          |

## rooms

> To get all escape room sessions played, use this GraphQL query (`GET` method):

```javascript
query {
  rooms {
    name
    playedDatetime
    durationTime
    numberOfHints
  }
}
```

> Expected response:

```json
{
  "data": {
    "roomSessions": [
      {
        "name": "Escape Room Toulouse",
        "playedDatetime": "2001-01-01T12:00:00+00:00",
        "durationTime": 3000.0,
        "numberOfHints": 2
      }
    ]
  }
}
```
