# Patrons

## Login

```shell
curl "https://phrenzi.com/api/v1/patrons/sign_in"
  -H "Authorization: app_token"
  -X POST
  -d '{
        "email": "abc@gmail.com",
        "password": "password" }'
```

> The above command returns `User` object structured like this:

```json
{
  "id": "ADSFSDA",
  "name": "Simon Iong",
  "email": "abc@example.com",
  "credit_balance": 233.23,
  "token": "adafasdszdads"
}
```

This endpoint authenticate by `app_token`, and try to authenticate Patron.

* if success, it will return `Patron` object with HTTP Status Code `201`, then client can use token in that object to consume other apis for Patron only.
* if failed to authenticate, it will return HTTP Status Code `401`
* if user authenticate failed too many time, it will return HTTP Status Code `429`

TODO: figure out what to do if user authenticate fail too many times.

### HTTP Request

`POST http://example.com/api/v1/patrons/sign_in`

### Query Parameters

Parameter | Description
--------- | -----------
email | the email of patron account
password | the password of patron account

## Sign Up

```shell
curl "http://example.com/api/v1/patrons/sign_up"
  -H "Authorization: app_token"
```

> The above command returns HTTP Status Code `201` if success.

This endpoint authenticate by `app_token`, and try to register a account for Patron.

* if success, it will return HTTP Status Code `201` without any json object
* if failed, it will return HTTP Status Code `422`

TODO: figure out if we need to show validation errors message by different fields

### HTTP Request

`POST http://phrenzi.com/api/patrons/sign_up`

### URL Parameters

Parameter | Description
--------- | -----------
name | the name of patron
email | the email of patron
password | the password of patron account
password_confirmation | confirm password again

## Forget Password

```shell
curl "http://example.com/api/patrons/forget_password"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`POST http://phrenzi.com/api/patrons/sign_up'

### URL Parameters

Parameter | Description
--------- | -----------
email | the email of patron
password | the password of patron account
password_confirmation | confirm password again