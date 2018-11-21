# Management / Staffs

## Get all staffs


```shell
curl "https://phrenzi.com/api/management/staffs" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
```

> The above command returns array of `Staff` object like this:

```json
{
  "staffs": [
    {
      "id": "828055eb-a94d-4f71-aa90-110d5b747468",
      "first_name": "first1",
      "last_name": "last1",
      "manager": true,
      "setuped": true
    },
    {
      "id": "10efd10c-22dc-4871-83cc-e8a36c103c85",
      "first_name": "first2",
      "last_name": "last2",
      "manager": false,
      "setuped": false
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and retrieves all staffs.

### HTTP Request

`GET http://phrenzi.com/api/management/staffs`

## Delete staff

```shell
curl "https://phrenzi.com/api/management/staffs/828055eb-a94d-4f71-aa90-110d5b747468" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X DELETE
```

> The above command returns 200 status code and empty json

This endpoint authenticated by `Manager Token`, and remove staff.

> if not authenticate, return 401 status code and following json message:

``` json
{
  "errors": [
    "You need to sign in or sign up before continuing."
  ]
}
```

### HTTP Request

`DELETE http://phrenzi.com/api/management/staffs/#{staff_id}`

## Staff Setup

```shell
curl "https://phrenzi.com/api/management/staffs/10efd10c-22dc-4871-83cc-e8a36c103c85/setup" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"\
  -X PATCH \
  -d '{
    "pin_code": "1234"
    }'
```

> The above command returns `Staff` object like this and status code 200 if success:

```json
{
  "staff": {
    "id": "10efd10c-22dc-4871-83cc-e8a36c103c85",
    "first_name": "first1",
    "last_name": "last1",
    "manager": true,
    "setuped": true
  }
}
```

> If requested staff is not found, return 404 and json response:

```json
{
  "errors": [
    "Staff not found"
  ]
}
```

> If requested setup is fail, return 422 and json response:

```json
{
  "errors": [
    "Pin code must be 4 digit"
  ]
}
```

> If requested staff already been setup, return 406 and json response:

```json
{
  "errors": [
    "Staff setup already"
  ]
}
```

This endpoint authenticated by `Manager Token`, and setup staff's pin_code

### HTTP Request

`PATCH http://phrenzi.com/api/management/staffs/:staff_id/setup`

### Query Parameters

Parameter | Description
--------- | -----------
pin_code | the pin code of staff, need to be 4 digit lenght

## Staff Sign In

```shell
curl "https://phrenzi.com/api/management/staffs/sign_in" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"\
  -X POST \
  -d '{
    "staff_id": "10efd10c-22dc-4871-83cc-e8a36c103c85",
    "pin_code": "1234"
    }'
```

> The above command returns `Staff` object like this and status code 200 if success:

```json
{
  "staff": {
    "id": "10efd10c-22dc-4871-83cc-e8a36c103c85",
    "first_name": "first1",
    "last_name": "last1",
    "manager": true,
    "setuped": true
  }
}
```

> If sign in failed, return status code 422 and response:

```json
{
  "errors": [
    "Pin code is invalid."
  ]
}
```

> If requested staff not found, return 404 not_found, and response:

```json
{
  "errors": [
    "Staff not found"
  ]
}
```

> If requested staff do not setup yet, return 479, and response:

```json
{
  "errors": [
    "Staff not setup yet"
  ]
}
```

This endpoint authenticated by `Manager Token`, and sign in staff

### HTTP Request

`POST http://phrenzi.com/api/management/staffs/sign_in`

### Query Parameters

Parameter | Description
--------- | -----------
staff_id | the uuid of staff
pin_code | the pin code of staff, need to be 4 digit lenght
