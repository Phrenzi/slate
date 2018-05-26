# Management / Sign Up

## Sign Up

```shell
curl "https://phrenzi.com/api/management/sign_up" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{
        "establishment_name": "Awesome Bar",
        "establishment_phone": "+85366762659",
        "manager_first_name": "Simon",
        "manager_last_name": "Iong",
        "email": "abc@example.com",
        "password": "password",
        "password_confirmation": "password" }'
```

> if success, the above command returns `Manager` object with `200` status code, and structured like this:

```json
{
  "manager": {
    "id": "d603ac2a-beae-4bd2-ae31-05db4895c001",
    "email": "abc@example.com",
    "first_name": "Simon",
    "last_name": "Iong",
    "establishment_name": "Awesome Bar",
    "establishment_setup": false
  }
}
```

> if failed, the above command returns status code `422` and json object with error message like this:

``` json
{
  "errors": [
    "Manager first name can't be blank"
  ]
}
```

> if token is invalid, return 401 and following json object

``` json
{
  "errors": [
    "Bad credentials"
  ]
}
```

This endpoint is for sign up, and need App Token authenticated.

* if success, it will return `Manager` object with HTTP Status Code `200`
* if failed to authenticate, it will return HTTP Status Code `401` with `errors` message.

### HTTP Request

`POST http://example.com/api/management/sign_up`

### Query Parameters

Parameter | Description
--------- | -----------
establishment_name | Name of Establishment
establishment_phone | Phont of Establishment
manager_first_name | Manager First Name
manager_last_name | Manager Last Name
email | Manager's email
password | Manager's password
password_confirmation | Manager's password confirmation
