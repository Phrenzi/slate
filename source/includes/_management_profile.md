# Management / Profile

## Update brand

```shell
curl "https://phrenzi.com/api/management/profile/brand" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "establishment_name": "Awesome Bar",
    "desc": "Desc",
    "contact_phone": "66762659",
    "contact_first_name": "Simon",
    "contact_last_name": "Iong",
    "max_payout_rank": 10,
    "prize_percentage": 30
    }'
```

> if success, returns HTML status code 200 OK, with empty json

> if error, return HTML status code 422, with following json:

```json
{
  "errors": [
    "Max payout rank can't be blank",
    "Max payout rank is not a number"
  ]
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

This endpoint authenticated by `Manager Token`, and update cash_back for current establishment.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`PATCH http://phrenzi.com/api/management/profile/brand`

### Query Parameters

Parameter | Description
--------- | -----------
establishment_name | Establishment Name
desc | Description of Establishment
contact_phone | contact phone of Establishment
contact_first_name | Contact First name
contact_last_name | Contact Last name
max_payout_rank | Default Maximum Payout Ranking setting
prize_percentage | Default Prize percentage

## Update Address

```shell
curl "https://phrenzi.com/api/management/profile/address" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "street1": "Street 1",
    "street2": "Street 2",
    "city": "Mawan",
    "country": "HK",
    "lat": 123.3223323,
    "long": 123.3223323
    }'
```

> If success, return http status code `200` with empty json object

> if error return 422, and following json object:

```json
{
  "errors": [
    "Street1 can't be blank"
  ]
}
```

This endpoint authenticated by `Manager Token`, and update profile address

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`PATCH http://phrenzi.com/api/management/profile/address`

### Query Parameters

Parameter | Description
--------- | -----------
street1 | Street address 1
street2 | Street address 2
city | City of Establishment
country | Country code of Establishment
lat | latitude of Establishment
long | longtitude of Establishment
