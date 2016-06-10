# Patrons

## Sign Up

```shell
curl "http://phrenzi.com/api/patrons" \
  -H "Content-Type: application/json" \
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
      "credit-balance": "0.0"
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
      "credit-balance": "233.23"
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

```shell
curl "https://phrenzi.com/api/patrons/confirmation" \
  -X GET
  -d '{
    "confirmation_token": "abcasdfasd",
    "redirect_url": "phrenzi://",
    "config": "default"
    }'
```

> if success, it will redirect to the `redirect_url` specify in this api

> if failed, it will raise an exception ActionController::RoutingError

during sign up procedure of patron ( client call Patron sign up API ),
server will sent out a confirmation email to Patron's mailbox,
patron will need to click a link in that email,
there's a generated confirmation_token in there, which will be use to call
in this endpoint.

<aside class="warning">Client don't need to call this API.</aside>

### HTTP Request

`GET http://example.com/api/patrons/confirmation`

### Query Parameters

Parameter | Description
--------- | -----------
confirmation_token | the confirmation token for patron
redirect_url | the params is pass-in from patron sign up API
config | the config object, which is `default`

## Request Reset Password

```shell
curl "http://example.com/api/patrons/passwords" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{
        "email": "abc@gmail.com" }'
        "redirect_url": "phrenzi://" }'
```

> if success, return HTTP Status Code `200` without following json object

``` json
{
  "success": true,
  "message": "An email has been sent to 'abc@gmail.com' containing instructions for resetting your password."
}
```

> if email not found, return HTTP Status Code `404, with following json object

``` json
{
  "success": false,
  "errors": [ "Unable to find user with email 'abc@gmail.com.'" ]
}
```

> if email is missing, return HTTP Status Code `401`, with following json object

``` json
{
  "success": false,
  "errors": ["You must provide an email address."]
}
```

> if redirect_url is missing, return HTTP Status Code `401`, with following json object

``` json
{
  "success": false,
  "errors": [ "Missing redirect URL." ]
}
```

This api is used while Patron forget password, and after this api is invoked and is success, a email
will trigger and sent to Patron's registered email

* if success, it will return HTTP Status Code `200` without json object
* if email is missing, it will return HTTP Status Code `401`
* if redirect_url is missing, it will return HTTP Status Code `401`
* if email is not found in server, it will return HTTP Status Code `404`

### HTTP Request

`POST http://phrenzi.com/api/patrons/passwords`

### URL Parameters

Parameter | Description
--------- | -----------
email | the email of patron
redirect_url | the url that is used within reset password email to redirect back to app

## Password Reset Link

```shell
curl "https://phrenzi.com/api/patrons/password/edit" \
  -H "Content-Type: application/json" \
  -X GET \
  -d '{
    "reset_password_token": "abcasdfasd",
    "redirect_url": "phrenzi://"
    }'
```

> if success, it will redirect to the `redirect_url` specify in this api

> if failed, it will raise an exception ActionController::RoutingError

during password reset procedure of patron ( client call Patron request password reset API ), server
will sent out a password reset email to Patron's mailbox,
patron will need to click a link in that email,
which will trigger this call if Patron click that link.
If every thing is fine, Patron will redirect to app,
with `auth header` in a request, then App can
retrieve `auth header` from that redirect request.

<aside class="warning">Client don't need to call this API.</aside>

### HTTP Request

`GET http://phrenzi.com/api/patrons/password/edit`

### URL Parameters

Parameter | Description
--------- | -----------
reset_password_token | reset password token
redirect_url | a link to redirect back after success operation

## Update Password

```shell
curl "https://phrenzi.com/api/patrons/password" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X PATCH \
  -d '{
    "password": "new_password",
    "password_confirmation": "new_password"
    }'
```

> if success, it will response with http status code `200`, and with following json object

``` json
{
  "success": true,
  "message": "Your password has been successfully updated."
}
```

> if failed, for example, password mismatch, response with http status code `422`,
and with following json object

``` json
{
  "success": false,
  "errors": {
    "password_confirmation": ["doesn't match Password"],
    "full_messages": ["Password confirmation doesn't match Password"]
  }
}
```

> if not authenticate, response with `401` and following json object,

``` json
{
  "success": false,
  "errors": ["Unauthorized"]
}
```

This api endpoint need Patron authenticated.

* if success, response with http status code `200`
* if authenticate failed, response with http status code `401`
* if validation failed, for example, passsord mismatch, response with http status code `422`

### HTTP Request

`PATCH http://phrenzi.com/api/patrons/password`

### URL Parameters

Parameter | Description
--------- | -----------
password | the new password of patron
password_confirmation | confirm again the new password
