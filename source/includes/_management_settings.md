# Management / Settings

## Get cash back

```shell
curl "https://phrenzi.com/api/management/settings/cash_back" \
  -H "Content-Type: application/json" \
```

> if success, return http status code 200 with following json object:

```json
{
  "data": {
    "id": "452d66ba-1796-4cbc-97dd-9a52830beefa",
    "type": "establishments",
    "attributes": {
      "cash-back": "3.5"
    }
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
  "data": {
    "id": "36bc3564-81d5-43cc-96e9-a34e405baadb",
    "type": "establishments",
    "attributes": {
      "cash-back": "4.5"
    }
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
  -H "Authorization: manager_token" \
  -X PATCH \
  -d '{
    "current_password": "current_password",
    "password": "new_password",
    "password_confirmation": "new_password"
    }'
```

> The above command returns HTML status code 200 OK

This endpoint require `manager_token`, and update current password for current manager.

### HTTP Request

`PATCH http://phrenzi.com/api/management/settings/update_password`

### Query Parameters

Parameter | Description
--------- | -----------
current_password | the current password for current manager
password | the new password for current manager
password_confirmation | confirmation for the new password
