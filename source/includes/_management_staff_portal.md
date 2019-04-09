# Management / Staffs Portal

## Create staff

```shell
curl "https://phrenzi.com/api/management/portal/staffs" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token"\
  -X POST \
  -d '{
    "first_name": "Simon",
    "last_name": "Iong",
    "manager": true
    }'
```

> The above command returns with 200 ok status code and with `Staff` object like this:

```json
{
  "staff": {
    "id": "451dad93-71c4-4f8e-8709-ce3faa43e1c8",
    "first_name": "Simon",
    "last_name": "Iong",
    "setuped": false,
    "manager": true
  }
}
```

> If error happened, return 422 status code, and json object:

``` json
{
  "errors": [
    "First name can't be blank"
  ]
}
```

This endpoint authenticated by `Access Token`, and update staffs.

### HTTP Request

`POST http://phrenzi.com/api/management/portal/staffs`

### Query Parameters

Parameter | Description
--------- | -----------
first_name | first_name of Staff
last_name | last_name of Staff
manager | true or false

## Update staff

```shell
curl "https://phrenzi.com/api/management/portal/staffs/10efd10c-22dc-4871-83cc-e8a36c103c85" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token"\
  -X PATCH \
  -d '{
    "first_name": "Simon",
    "last_name": "Iong",
    "manager": true
    }'
```

> The above command returns with 200 ok status code and with `Staff` object like this:

```json
{
  "staff": {
    "id": "451dad93-71c4-4f8e-8709-ce3faa43e1c8",
    "first_name": "Simon",
    "last_name": "Iong",
    "setuped": false,
    "manager": true
  }
}
```

> If error happened, return 422 status code, and json object:

``` json
{
  "errors": [
    "First name can't be blank"
  ]
}
```

This endpoint authenticated by `Access Token`, and update staffs.

### HTTP Request

`PATCH http://phrenzi.com/api/management/portal/staffs/:staff_id`

### Query Parameters

Parameter | Description
--------- | -----------
first_name | first_name of Staff
last_name | last_name of Staff
manager | true or false

## Reset Staff Pin Code

```shell
curl "https://phrenzi.com/api/management/portal/staffs/10efd10c-22dc-4871-83cc-e8a36c103c85/reset_pin" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token"\
  -X PATCH
```

> The above command returns `Staff` object like this and status code 200 if success:

```json
{
  "staff": {
    "id": "0eda8237-872e-4787-ba20-8a421b226871",
    "first_name": "first1",
    "last_name": "last1",
    "setuped": false,
    "manager": true
  }
}
```

> If requested staff is not setup yet, return 479 and json response:

```json
{
  "errors": "Staff is not setup yet"
}
```

This endpoint authenticated by `Access Token`, and reset staff's pin_code

### HTTP Request

`PATCH http://phrenzi.com/api/management/portal/staffs/:staff_id/reset_pin`

## Delete staff

```shell
curl "https://phrenzi.com/api/management/portal/staffs/828055eb-a94d-4f71-aa90-110d5b747468" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -X DELETE
```

> The above command returns 200 status code and empty json

This endpoint authenticated by `Access Token`, and remove staff.


> if not authenticate, return 401 status code and following json message:

``` json
{
  "errors": [
    "You need to sign in or sign up before continuing."
  ]
}
```

### HTTP Request

`DELETE http://phrenzi.com/api/management/portal/staffs/#{staff_id}`
