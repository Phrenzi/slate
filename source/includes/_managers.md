# Managers

## Sign In

```shell
curl "https://phrenzi.com/api/managers/oauth/token" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{
        "email": "abc@gmail.com",
        "password": "password",
        "grant_type: "password",
        "user_type": "manager" }'
```

> if success, the above command returns `Manager` object with `200` status code, and structured like this:

```json
{
  "manager": {
    "id": "e31dfa53-6fb4-4053-b6bc-f20d839fba74",
    "email": "manager1@gmail.com",
    "first_name": "manager1",
    "last_name": "manager1",
    "establishment_name": "Establishment1",
    "establishment_setup": true,
    "access_token": "d0d0ac5d26238b769f7895d3faacb532ad455f0c113bcbdd3a92a9e585db5c38",
    "token_type": "Bearer",
    "expires_in": 2629746,
    "refresh_token": "b01f5245e5c1402a0e970921ef01c987f2a75cce8914462b41a5fffdb6a20028",
    "created_at": 1555065566
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
  "errors": ["A confirmation email was sent to your email. You must follow the instructions in the email before your account can be activated"]
}
```

This endpoint try to authenticate Manager using Oauth "Resource Owner Password Credentials".

* if success, it will return object with access_token and HTTP Status Code `200`, and client can consuming any protected (start with management namespace ) request with this access token.
* if failed to authenticate, it will return HTTP Status Code `401` with `errors` message.

### HTTP Request

`POST http://example.com/api/managers/oauth/token`

### Query Parameters

Parameter | Description
--------- | -----------
email | the email of manager account
password | the password of manager account
grant_type | must be "password"
user_type | must be "manager"

## Sign Out

```shell
curl "https://phrenzi.com/api/managers/oauth/revoke" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X POST
```

> if success, the above command returns status code `200`, and json object like this:

```json
{}
```

> if failed, either token is missing, token is expired, or token not found, the above command returns status code `200` as well, with empty json object

``` json
{
}
```

this endpoint authenticated by `Access Token`, you are going to get it from Manager `Sign In` api request.

* if success, it will return HTTP Status Code `200`, and revoke access_token
* if failed, it will return HTTP Status Code `200` as well, but not revoke access_token

### HTTP Request

`POST http://example.com/api/managers/revoke`

## Resend Confirmation Email

```shell
curl "https://phrenzi.com/api/managers/confirmation" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{ "email": "abc@gmail.com" }'
```

> if success, the above command returns `Manager` object with `200` status code, and structured like this:

```json
{
  "messages": [
    "An email has been sent to 'abc@gmail.com' containing instructions for activate your account."
  ]
}
```


> if email is missing, return status code `422` and json object:


``` json
{
  "errors": [
    "You must provide an email address."
  ]
}
```

> if manager with request email can not been found, return status code `404` and json like this:

``` json
{
  "errors": [
    "Unable to find user with email 'abc@gmail.com'."
  ]
}
```

> if manager is already confirmed, return status code `406` and json like this:

``` json
{
  "errors": [
    "Already confirmed."
  ]
}
```

This endpoint try to authenticate Manager, and need App Token authenticated.

### HTTP Request

`POST http://example.com/api/managers/confirmation`

### Query Parameters

Parameter | Description
--------- | -----------
email | the email of manager
