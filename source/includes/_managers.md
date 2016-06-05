# Managers

## Login

```shell
curl "https://phrenzi.com/api/v1/managers/sign_in"
  -H "Authorization: app_token"
  -X POST
  -d '{
        "email": "abc@gmail.com",
        "password": "password" }'
```

> The above command returns `Manager` object with HTTP Status Code `201`

```json
{
  "id": "ADSFSDA",
  "name": "Simon Iong",
  "email": "abc@example.com",
  "token": "adafasdszdads"
}
```

This endpoint authenticate by `app_token`, and try to authenticate Manager.

* if success, it will return `Manager` object with HTTP Status Code `201`, then client can use token in that object to consume other apis for Manager only.
* if failed to authenticate, it will return HTTP Status Code `401`
* if manager authenticate failed too many time, it will return HTTP Status Code `429`

TODO: figure out what to do if user authenticate fail too many times.

### HTTP Request

`POST http://example.com/api/v1/managers/sign_in`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
email | N/A | the email of patron account
password | N/A | the password of patron account
