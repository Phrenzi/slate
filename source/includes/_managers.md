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
    "email": "abc@gmail.com"
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
  "success": false,
  "errors": ["A confirmation email was sent to your account at 'abc@gmail.com'. You must follow the instructions in the email before your account can be activated"]
}
```

This endpoint try to authenticate Manager

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

this endpoint need `Auth Header` to authenticate manager,
you are going to get it from Manager `Sign In` api request
or other subsequence request that need authentication.

* if success, it will return HTTP Status Code `200`
* if failed to authenticate, it will return HTTP Status Code `404` with `errors` message.

### HTTP Request

`DELETE http://example.com/api/managers/sign_out`
