# Patrons

## Sign Up

```shell
curl "http://phrenzi.com/api/patrons" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{
        "first_name": "Simon",
        "last_name": "Iong",
        "email": "abc@gmail.com",
        "password": "password",
        "password_confirmation": "password",
        "confirm_success_url": "phrenzi://"
        }'
```

> if success, the above command returns HTTP Status Code `200` with following json objects:

```json
{
  "patron": {
    "id": "37f335c5-a88c-41a3-a643-fba688c72897",
    "first_name": "Simon",
    "last_name": "Iong",
    "email": "abc@example.com",
    "trans_code": "8cc897"
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

This endpoint try to register a account for Patron, and need App Token authenticate.

* if success, it will return HTTP Status Code `200` with `Patron` json object
* if failed, it will return HTTP Status Code `422`, and with `errors` json message

### HTTP Request

`POST http://phrenzi.com/api/patrons`

### URL Parameters

Parameter | Description
--------- | -----------
first_name | the first name of patron
last_name | the last name of patron
email | the email of patron
password | the password of patron account
password_confirmation | confirm password again
confirm_success_url | the url after confirmation link is click


## Sign In

```shell
curl "https://phrenzi.com/api/patrons/sign_in" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{
        "email": "abc@gmail.com",
        "password": "password" }'
```

> if success, the above command returns `Patron` object with `200` status code, and structured like this:

```json
{
  "patron": {
    "id": "288f4f0f-da30-45c4-a531-c0a804628395",
    "name": "Simon Iong"
    "first_name": "Simon",
    "last_name": "Iong",
    "email": "abc@gmail.com",
    "trans_code": "76efd7",
    "token": "f1b811b47dc44cbeb8a03b9021f76ac4",
    "token_exp_at": 1506672320,
    "refresh_token": "2c74332c27df44b884b06714f0110f23",
    "refresh_token_exp_at": 1509177920
  }
}
```

> if failed, the above command returns status code `401` and json structured like this:

``` json
{
  "errors": [ "Invalid login credentials. Please try again." ]
}
```

> if patron is not confirmed yet, return status code `401` and json like this:

``` json
{
  "errors": ["A confirmation email was sent to your account at 'abc@gmail.com'. You must follow the instructions in the email before your account can be activated"]
}
```

This endpoint try to authenticate Patron, and need App Token authenticate.

* if success, it will return `Patron` object with HTTP Status Code `200`, and client can retrive
Patron Token pair from reponse to consuming `patron_app` namespace APIs.
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
  -H "Authorization: token" \
  -X DELETE
```

> if success, the above command returns status code `200`, and json object like this:

```json
{
  "messages": [
    "successfully logout!"
  ]
}
```

> if failed, the above command returns status code `404`, and errors json like this:

``` json
{
  "errors": ["User was not found or was not logged in."]
}
```

this endpoint need `Patron Token` to authenticate patron,
you can retrieve it from Patron `Sign In` api request, or Patron `Token` api.

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

## Request Reset Password

```shell
curl "http://example.com/api/patrons/password" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{
        "email": "abc@gmail.com" }'
        "redirect_url": "phrenzi://" }'
```

> if success, return HTTP Status Code `200` without following json object

``` json
{
  "messages": ["An email has been sent to 'abc@gmail.com' containing instructions for resetting your password."]
}
```

> if email not found, return HTTP Status Code `404, with following json object

``` json
{
  "errors": [ "Unable to find user with email 'abc@gmail.com.'" ]
}
```

> if email is missing, return HTTP Status Code `401`, with following json object

``` json
{
  "errors": ["You must provide an email address."]
}
```

> if redirect_url is missing, return HTTP Status Code `401`, with following json object

``` json
{
  "errors": [ "Missing redirect URL." ]
}
```

This api need App Token authenticated and is used while Patron forget password, and after this api is invoked and is success, a email
will trigger and sent to Patron's registered email.

* if success, it will return HTTP Status Code `200` without json object
* if email is missing, it will return HTTP Status Code `401`
* if redirect_url is missing, it will return HTTP Status Code `401`
* if email is not found in server, it will return HTTP Status Code `404`

### HTTP Request

`POST http://phrenzi.com/api/patrons/password`

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

> if success, it will redirect to the `redirect_url` specify in this api, and with Patron's token attached

```bash
phrenzi://?token=xxxxx
```

> if failed, it will return with status_code 404, and folloing json:

```json
{
  "errors": ["not found!"]
}
```

during password reset procedure of patron ( client call Patron request password reset API ), server
will sent out a password reset email to Patron's mailbox,
patron will need to click a link in that email,
which will trigger this call if Patron click that link.
If every thing is fine, Patron will redirect to app,
with Patron token's `token` in a request, then App can
retrieve `token` from that redirect request.

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
  -H "Authorization: token" \
  -X PATCH \
  -d '{
    "password": "new_password",
    "password_confirmation": "new_password"
    }'
```

> if success, it will response with http status code `200`, and with following json object

``` json
{
  "messages": ["Your password has been successfully updated."]
}
```

> if failed, for example, password mismatch, response with http status code `422`,
and with following json object

``` json
{
  "errors": {
    "password_confirmation": ["doesn't match Password"],
    "full_messages": ["Password confirmation doesn't match Password"]
  }
}
```

> if not authenticate, response with `401` and following json object,

``` json
{
  "errors": ["Unauthorized"]
}
```

This api endpoint need `Patron Token` authenticated.

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

## Token Exchange

```shell
curl "https://phrenzi.com/api/patrons/token" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X POST
```

> if success, it will response with http status code `200`, and with following json object

``` json
{
  "patron": {
    "id": "314e7168-fe41-4d67-b945-209a3439d7f0",
    "name": "Patron1",
    "first_name": "Patron",
    "last_name": "Last Name",
    "email": "patron1@gmail.com",
    "trans_code": "ec6eec",
    "profile": null,
    "token": "918cf11feba34a58a2f4b8860fb87c60",
    "token_exp_at": 1506677658,
    "refresh_token": "c6246969fdbb4013a41d5ed04f26e491",
    "refresh_token_exp_at": 1509183258
  }
}
```

> if failed, for example, refresh token is missing or not found, or even refresh token is valid, but expired, response with http status code `401`,
and with following json object

``` json
{
  "errors": [
    "You need to sign in or sign up before continuing."
  ]
}
```

This api endpoint authenticated by `Patron Token`'s `refresh_token`, and will exchange with a new pair of `Patron Token`

* if success, response with http status code `200`
* if authenticate failed, response with http status code `401`

### HTTP Request

`POST http://phrenzi.com/api/patrons/token`
