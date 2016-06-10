# Patrons

## Sign Up

```shell
curl "http://phrenzi.com/api/patrons" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{
        "name": "Simon",
        "email": "abc@gmail.com",
        "password": "password",
        "password_confirmation": "password",
        "confirm_success_url": "phrenzi://"
        }'
```

> if success, the above command returns HTTP Status Code `200` with following json objects:

```json
{
  "data": {
    "id": "ABCDDD",
    "type": "patrons",
    "attributes": {
      "name": "Simon",
      "email": "abc@gmail.com",
      "credit_balance": 0.0
    }
  }
}
```

> if failed, the above command returns HTTP Status Code `422` with following json objects:

``` json
{
  "errors": {
    "email": ["already in use"],
    "full_messages": ["Email already in use"]
  }
}
```

This endpoint try to register a account for Patron.

* if success, it will return HTTP Status Code `200` with `Patron` json object
* if failed, it will return HTTP Status Code `422`, and with `errors` json message

### HTTP Request

`POST http://phrenzi.com/api/patrons`

### URL Parameters

Parameter | Description
--------- | -----------
name | the name of patron
email | the email of patron
password | the password of patron account
password_confirmation | confirm password again
confirm_success_url | the url after confirmation link is click


## Sign In

```shell
curl "https://phrenzi.com/api/patrons/sign_in" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{
        "email": "abc@gmail.com",
        "password": "password" }'
```

> if success, the above command returns `Patron` object with `200` status code, and structured like this:

```json
{
  "data": {
    "id": "ADSFSDA",
    "attributes": {
      "name": "Simon Iong",
      "email": "abc@example.com",
      "credit_balance": 233.23
    }
  }
}
```

> if failed, the above command returns status code `401` and json structured like this:

``` json
{
  "errors": [ "Invalid login credentials. Please try again." ]
}
```

This endpoint try to authenticate Patron

* if success, it will return `Patron` object with HTTP Status Code `200`, and client can retrive
auth header from reponse to consuming next request that need authentication.
* if failed to authenticate, it will return HTTP Status Code `401` with `errors` message.

### HTTP Request

`POST http://example.com/api/patrons/sign_in`

### Query Parameters

Parameter | Description
--------- | -----------
email | the email of patron account
password | the password of patron account


## Sign Out

```shell
curl "https://phrenzi.com/api/patrons/sign_out" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com"
  -X DELETE
```

> if success, the above command returns status code `200`, and json object like this:

```json
{
  "success": true
}
```

> if failed, the above command returns status code `404`, and errors json like this:

``` json
{
  "errors": ["User was not found or was not logged in."]
}
```

this endpoint need `Auth Header` to authenticate patron,
you are going to get it from Patron `Sign In` api request
or other subsequence request that need authentication.

* if success, it will return HTTP Status Code `200`
* if failed to authenticate, it will return HTTP Status Code `404` with `errors` message.

### HTTP Request

`DELETE http://example.com/api/patrons/sign_out`

## Confirmation Patron

client don't need to call this api, pending for more information

## Forget Password ( Not Done yet )

```shell
curl "http://example.com/api/patrons/passwords" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{
        "email": "abc@gmail.com" }'
```

> The above command returns HTTP Status Code `200` without any json object

This endpoint authenticate by `app_token`, and try to reset password

* if success, it will return HTTP Status Code `200` without any json object
* if failed, it will return HTTP Status Code `422`, with json message: "There's an error resetting password"

### HTTP Request

`POST http://phrenzi.com/api/patrons/passwords`

### URL Parameters

Parameter | Description
--------- | -----------
email | the email of patron
