# Management / Settings

## Get cash back

```shell
curl "https://phrenzi.com/api/management/settings/cash_back" \
  -H "Content-Type: application/json" \
```

> if success, return http status code 200 with following json object:

```json
{
  "setting": {
    "cash_back": "3.5"
  }
}
```

> if failed, for example, unauthorized, then return http status code 401 with following json object:

``` json
{
  "errors": [
    "Authorized users only."
  ]
}
```

This endpoint require `manager authenticate`

### HTTP Request

`GET http://phrenzi.com/api/management/cash_back`

## Update cash back

```shell
curl "https://phrenzi.com/api/management/settings/cash_back" \
  -H "Content-Type: application/json" \
  -X PATCH \
  -d '{
    "password": "current_password",
    "cash_back": 4.5
    }'
```

> if success, returns HTML status code 200 OK, with following object:

``` json
{
  "setting": {
    "cash_back": "4.5"
  }
}
```

> if unauthorize, returns HTML status code 401, with following object:

``` json
{
  "errors": [
    "Authorized users only."
  ]
}
```

> if password is invalid, return HTML status code 406, with following object:

``` json
{
  "errors": [
    "Invalid Password"
  ]
}
```

This endpoint require manager authenticate, and update cash_back for current establishment.

### HTTP Request

`PATCH http://phrenzi.com/api/management/cash_back`

### Query Parameters

Parameter | Description
--------- | -----------
cash_back | the cash_back to update, within 0 and 100
password | the current password for current manager

## Update Password

```shell
curl "https://phrenzi.com/api/management/settings/passwords" \
  -H "Content-Type: application/json" \
  -X PATCH \
  -d '{
    "current_password": "current_password",
    "password": "new_password",
    "password_confirmation": "new_password"
    }'
```

> If success, return http status code `200` with following json object

``` json
{
  "manager": {
    "id": "2544a3af-cda6-4a0d-b760-17e43e1cc165",
    "email": "manager1@gmail.com"
  }
}
```

> if failed, return http status code `422`, with following json object

``` json
{
  "errors": {
    "current_password": [ "is invalid" ],
    "password_confirmation": [ "doesn't match Password" ]
  }
}
```

This endpoint require `manager_token`, and update current password for current manager.

### HTTP Request

`PATCH http://phrenzi.com/api/management/settings/update_password`

### Query Parameters

Parameter | Description
--------- | -----------
current_password | the current password for current manager
password | the new password for current manager
password_confirmation | confirmation for the new password
