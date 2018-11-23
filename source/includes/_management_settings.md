# Management / Settings

## Get cash back

```shell
curl "https://phrenzi.com/api/management/settings/cash_back" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> if success, return http status code 200 with following json object:

```json
{
  "setting": {
    "cash_back": "3.5"
  }
}
```

> if staff is not login, return status code 479, and following json:

```json
{
  "errors": [
    "Staff not signed in"
  ]
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

This endpoint require `Manager Token` and return cash back settings

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>


### HTTP Request

`GET http://phrenzi.com/api/management/cash_back`

## Update cash back

```shell
curl "https://phrenzi.com/api/management/settings/cash_back" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
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

> if staff is not login, return status code 479, and following json:

```json
{
  "errors": [
    "Staff not signed in"
  ]
}
```

> if staff is not a manager, return status code 479, and following json:

```json
{
  "errors": "Current Staff is not a manager"
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

This endpoint authenticated by `Manager Token`, and update cash_back for current establishment.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`PATCH http://phrenzi.com/api/management/cash_back`

### Query Parameters

Parameter | Description
--------- | -----------
cash_back | the cash_back to update, within 0 and 100
password | the current password for current manager

## Update Password

```shell
curl "https://phrenzi.com/api/management/settings/password" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
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
    "email": "manager1@gmail.com",
    "establishment_name": "Awesome Bar"
  }
}
```

> if staff is not login, return status code 479, and following json:

```json
{
  "errors": [
    "Staff not signed in"
  ]
}
```

> if staff is not a manager, return status code 479, and following json:

```json
{
  "errors": "Current Staff is not a manager"
}
```

> if failed, return http status code `422`, with following json object

``` json
{
  "errors": [
    "Current password is invalid",
    "Password confirmation doesn't match Password"
  ]
}
```

This endpoint authenticated by `Manager Token`, and update current password for current manager.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`PATCH http://phrenzi.com/api/management/settings/password`

### Query Parameters

Parameter | Description
--------- | -----------
current_password | the current password for current manager
password | the new password for current manager
password_confirmation | confirmation for the new password
