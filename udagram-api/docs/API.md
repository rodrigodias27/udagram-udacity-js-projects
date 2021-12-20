# API Documentation

- [API Documentation](#api-documentation)
  - [API Endpoint](#api-endpoint)
    - [Users](#users)
    - [Feed](#feed)
  - [API Data Shapes](#api-data-shapes)
      - [Users](#users-1)
      - [Feed](#feed-1)
  - [API endpoints (how to use)](#api-endpoints-how-to-use)
    - [POST /users/auth/login](#post-usersauthlogin)
      - [How to use user authentication:](#how-to-use-user-authentication)
    - [GET /users/auth/verification](#get-usersauthverification)
    - [GET /users/:id](#get-usersid)
    - [POST /users/auth](#post-usersauth)
    - [GET /feed](#get-feed)
    - [GET /feed/:id](#get-feedid)
    - [GET /feed/signed-url/:fileName](#get-feedsigned-urlfilename)
    - [POST /feed](#post-feed)

## API Endpoint

### Users
- [POST /users/auth/login - Login User](#post-usersauthlogin)
- [GET /users/auth/verification - Verify if user is authenticated](#get-usersauthverification)
- [GET /users/:id [token required] - Get user by id](#get-usersid)
- [POST /users/auth - Create user](#post-usersauth)

### Feed
- [GET /feed - Get all feeds](#get-feed)
- [GET /feed/:id - Get feed by id](#get-feedid)
- [GET /feed/signed-url:fileName [token required] - Get signed-url to put image on s3](#get-feedsigned-urlfilename)
- [POST /feed [token required] - Post a new feed](#post-feed)

## API Data Shapes

#### Users
- email: string
- passwordHash: string
- createdAt: string
- updatedAt: string

#### Feed
- id: number
- caption: string
- url: string
- createdAt: string
- updatedAt: string

## API endpoints (how to use)

---
### POST /users/auth/login
Return a jwt token to authenticate in other endpoints.

Body:
- email: email of user
- password: password defined on creation

```json
{
  "email": "doctor@who.com",
  "password": "Trenzalore"
}
```

**Response example**:
- Success `200 OK`
```json
{
  "auth": true,
  "token": "<jwt_token>",
  "user": {
    "email": "doctor@who.com"
  }
}
```

#### How to use user authentication:

Add jwt on headers:
```json
{"Authorization": "Bearer <jwt_token>"}
```
---
### GET /users/auth/verification
Verify if user is authenticated

```Obs.: Needs authentication```

**Response example**:
- Success `200 OK`
```json
{
  "auth": true,
  "message": "Authenticated."
}
```
---
### GET /users/:id
Return user according to id

Params:
- id: id of user

```Obs.: Needs authentication```

**Response example**:
- Success `200 OK`
```json
{
  "email": "doctor@who.com",
  "passwordHash": "<password_hash>",
  "createdAt": "2021-12-13T15:00:51.033Z",
  "updatedAt": "2021-12-13T15:00:51.033Z"
}
```
---
### POST /users/auth
Create an user

Body:
- email: email of user
- password: password to authenticate and get jwt_token

```json
{
  "email": "doctor@who.com",
  "password": "Trenzalore"
}
```

**Response example**:
- Success `200 OK`
```json
{
  "auth": true,
  "token": "<jwt_token>",
  "user": {
    "email": "doctor@who.com"
  }
}
```
---
### GET /feed
Return all posts on feed

**Response example**:
- Success `200 OK`
```json
{
  "count": 2,
  "rows": [
    {
      "id": 1,
      "caption": "Book and Glass",
      "url": "<image_url>",
      "createdAt": "2021-12-15T17:34:49.559Z",
      "updatedAt": "2021-12-15T17:34:49.560Z"
    },
    {
      "id": 2,
      "caption": "Universe",
      "url": "<image_url>",
      "createdAt": "2021-12-14T21:29:53.443Z",
      "updatedAt": "2021-12-14T21:29:53.443Z"
    }
  ]
}
```
---
### GET /feed/:id
Return post on feed according to id

Params:
- id: id of post

**Response example**:
- Success `200 OK`
```json
{
  "id": 1,
  "caption": "Ubuntu wallpaper",
  "url": "<image_url>",
  "createdAt": "2021-12-14T21:21:09.363Z",
  "updatedAt": "2021-12-14T21:21:09.364Z"
}
```
---
### GET /feed/signed-url/:fileName
Get an s3 signed-url to put image

Params:
- fileName: filename of image

```Obs.: Needs authentication```

**Response example**:
- Success `200 OK`
```json
{
  "url": "<signed_url>"
}
```
---
### POST /feed
Create a new post on feed

Body:
- caption: name of post
- url: url of image

```json
{
  "caption": "Ubuntu wallpaper",
  "url": "<image_url>",
}
```

```Obs.: Needs authentication```

**Response example**:
- Success `200 OK`
```json
{
  "id": 1,
  "caption": "Ubuntu wallpaper",
  "url": "<image_url>",
  "createdAt": "2021-12-14T21:21:09.363Z",
  "updatedAt": "2021-12-14T21:21:09.364Z"
}
```
