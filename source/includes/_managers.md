# Managers

## Sign In

```shell
curl "https://phrenzi.com/api/managers/sign_in" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{
        "email": "abc@gmail.com",
        "password": "password" }'
```

> if success, the above command returns `Manager` object with `200` status code, and structured like this:

```json
{
  "manager": {
    "id": "6b586aeb-a53d-476a-9435-659ed9547e6e",
    "email": "abc@gmail.com",
    "establishment_name": "Awesome Bar",
    "establishment_setup": true,
    "token": "494a1cff589247d2a0c5375033ac4314",
    "token_exp_at": "2017-09-30T04:50:10Z",
    "refresh_token": "a0d4a8c0c47341dc8acc725f66a9bfe8",
    "refresh_token_exp_at": "2017-10-29T04:50:10Z"
  }
}
```

> if failed, the above command returns status code `401` and json structured like this:

``` json
{
  "errors": [ "Invalid login credentials. Please try again." ]
}
```

> if manager is not confirmed yet, return status code `401` and json like this:

``` json
{
  "errors": ["A confirmation email was sent to your account at 'abc@gmail.com'. You must follow the instructions in the email before your account can be activated"]
}
```

This endpoint try to authenticate Manager, and need App Token authenticated.

* if success, it will return `Manager` object with HTTP Status Code `200`, and client can retrive
auth header from reponse to consuming next request that need authentication.
* if failed to authenticate, it will return HTTP Status Code `401` with `errors` message.

### HTTP Request

`POST http://example.com/api/managers/sign_in`

### Query Parameters

Parameter | Description
--------- | -----------
email | the email of manager account
password | the password of manager account


## Sign Out

```shell
curl "https://phrenzi.com/api/managers/sign_out" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X DELETE
```

> if success, the above command returns status code `200`, and json object like this:

```json
{
  "messages": ["successfully logout!"]
}
```

> if failed, either token is missing, token is expired, or token not found, the above command returns status code `401`, and errors json like this:

``` json
{
  "errors": [
    "You need to sign in or sign up before continuing."
  ]
}
```

this endpoint authenticated by `Manager Token`, you are going to get it from Manager `Sign In` api request.

* if success, it will return HTTP Status Code `200`
* if failed to authenticate, it will return HTTP Status Code `404` with `errors` message.

### HTTP Request

`DELETE http://example.com/api/managers/sign_out`
