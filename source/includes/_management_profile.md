# Management / Profile

## Get Profile

```shell
curl "https://phrenzi.com/api/management/profile" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> if success, returns HTML status code 200 OK, with empty json

```json
{
  "establishment": {
    "id": "84edd55b-26d4-4b2d-b8ca-92601c340f6d",
    "name": "Establishment1",
    "contact_first_name": "manager1",
    "contact_last_name": "manager1",
    "contact_phone": "612345671",
    "logo_url": "/uploads/cache/5a1df17481c893b5ae13660df0de9684.jpeg",
    "banner_url": "/uploads/cache/32a5272a2fdb5100402ff34365a777a1.jpeg",
    "desc": "This is an example description",
    "address": {
      "street1": "MyString",
      "street2": "MyString",
      "city": "MyString",
      "country": "MyString",
      "time_zone": "Asia/Macau"
    },
    "locations": [
      {
        "id": "7ce001bd-8268-4a42-85c5-93574b6a6015",
        "name": "location",
        "desc": "location desc",
        "lat": "1.2323",
        "long": "1.23333"
      },
      {
        "id": "01acdfe6-aaac-4caa-916d-df58c1e113ac",
        "name": "location",
        "desc": "location desc",
        "lat": "1.2323",
        "long": "1.23333"
      }
    ],
    "setting": {
      "max_payout_rank": 10
    },
    "business_hours": [
      {
        "id": "4d6fdd48-9309-4591-b421-800c5b1376c1",
        "wday": 0,
        "closed": false,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "id": "7412f175-721c-47da-a9f9-b0b18695c862",
        "wday": 1,
        "closed": false,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "id": "c513c75b-60d2-458b-8b20-5329a6847752",
        "wday": 2,
        "closed": false,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "id": "27c1a90b-8167-478f-8f97-c020cf543731",
        "wday": 3,
        "closed": false,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "id": "09bad649-bdd1-405e-966d-975c8168c962",
        "wday": 4,
        "closed": false,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "id": "08fae7f3-5053-4aea-93e1-d19bda14494e",
        "wday": 5,
        "closed": false,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "id": "919a0340-4016-46e0-944a-0698d3bdfe75",
        "wday": 6,
        "closed": false,
        "open_time": 39600,
        "close_time": 86400
      }
    ],
    "manager_staffs": [
      {
        "id": "4d1c7893-0a33-48d8-8cef-6e6557c20b2b",
        "first_name": "first1",
        "last_name": "last1",
        "manager": true,
        "setuped": false,
        "owner": false
      },
      {
        "id": "9b2cd8a9-ba70-4df7-8c49-307b3dfea7ff",
        "first_name": "first2",
        "last_name": "last2",
        "manager": false,
        "setuped": false,
        "owner": true
      }
    ],
    "favorite_patrons_count": 0,
    "setup": false,
    "setup_flags": {
      "brand": false,
      "address": false,
      "hours": false,
      "images": false,
      "billing": false,
      "terms": false
    },
    "current_challenge": {
      "start_date": "2016-12-06T16:00:00Z",
      "end_date": "2016-12-06T16:00:00Z",
      "prize_percentage": "25.0",
      "max_payout_rank": 5,
      "total_sales": "10000.0"
    }
}
```

This endpoint authenticated by `Access Token`, and get latest profile information for current establishment.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`GET http://phrenzi.com/api/management/profile`

## Update Brand

```shell
curl "https://phrenzi.com/api/management/profile/brand" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
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

This endpoint authenticated by `Access Token`, and update cash_back for current establishment.

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
  -H "Authorization: Bearer access_token" \
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

This endpoint authenticated by `Access Token`, and update profile address

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

## Pre-sign url for Logo & Banner

For profile logo

```shell
curl "https://phrenzi.com/profile_logo/cache/presign" \
  -H "Content-Type: application/json" \
```

For profile banner

```shell
curl "https://phrenzi.com/profile_banner/cache/presign" \
  -H "Content-Type: application/json" \
```

> The above command returns JSON structured like this:

```json
{
   "url" : "https://phrenzistaging.s3-ap-southeast-1.amazonaws.com",
   "fields" : {
      "policy" : "eyJleHBpcmF0aW9uIjoiMjAxNi0xMi0wOVQxMDoyNzozMVoiLCJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJwaHJlbnppc3RhZ2luZyJ9LHsia2V5IjoiY2FjaGUvMmE3OGI3MWI2MGYwMmZjMDk3YzFhYWM1ZTA0MDkxMzgifSx7IngtYW16LWNyZWRlbnRpYWwiOiJBS0lBSlhNM1U3QU02STNPRTM2QS8yMDE2MTIwOS9hcC1zb3V0aGVhc3QtMS9zMy9hd3M0X3JlcXVlc3QifSx7IngtYW16LWFsZ29yaXRobSI6IkFXUzQtSE1BQy1TSEEyNTYifSx7IngtYW16LWRhdGUiOiIyMDE2MTIwOVQwOTI3MzFaIn1dfQ==",
      "x-amz-algorithm" : "AWS4-HMAC-SHA256",
      "key" : "cache/2a78b71b60f02fc097c1aac5e0409138",
      "x-amz-signature" : "52956151623087d2a4997462c90055d61e51de3b1a5b8d89f826f1769da3894f",
      "x-amz-date" : "20161209T092731Z",
      "x-amz-credential" : "AKIAJXM3U7AM6I3OE36A/20161209/ap-southeast-1/s3/aws4_request"
   }
}
```

This endpoint retrieves pre-sign url for upload image into s3

### HTTP Request

`GET http://example.com/profile_#{logo|banner}/cache/presign`

After you retrive the presign url, you could be able to make a post request to presign url with the fields this end-point provided. Then you could be able to retrieve an id from S3. Please construct a json object with this id, and this object will going to be used in next API call to create the actual profile logo/banner in Phrenzi

For more detail, please visit shrine's plugin [direct_upload](http://shrinerb.com/rdoc/files/doc/direct_s3_md.html)

## Update Logo or Banner

```shell
curl "https://phrenzi.com/api/management/profile/images" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "logo":'{
          "id": "349234854924394", # required
          "storage": "cache", # required
          "metadata": {
            "size": 45461, # optional
            "filename": "foo.jpg", # optional
            "mime_type": "image/jpeg", # optional
          }
        }'
    }'
```

> If success, the above command returns status code 200 

> if image formet error, return 422 and following json object:

```json
{
  "errors": [
    "Logo isn't of allowed type (allowed types: image/jpg, image/jpeg, image/png, image/gif)"
  ]
}
```

This endpoint authenticated by `Access Token`, and update establishment profile logo or banner

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`PATCH http://phrenzi.com/api/management/profile/images`

### Query Parameters

Parameter | Description
--------- | -----------
banner | Banner image
logo | Logo image

## Update Business Hours

```shell
curl "https://phrenzi.com/api/management/profile/business_hours" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "business_hours": [
    {
      "id": "262bfa0f-325c-433d-95bc-3c418d1f3b31",
      "wday": 0,
      "closed": false,
      "extra_day": false,
      "open_time": 3600,
      "close_time": 86400
    },
    {
      "id": "e9a15246-8b7f-4e99-be65-9a3ca5d00e90",
      "wday": 1,
      "closed": false,
      "extra_day": false,
      "open_time": 3600,
      "close_time": 86400
    },
    {
      "id": "eb6728c3-d2f2-428c-aa98-e138481547c8",
      "wday": 2,
      "closed": false,
      "extra_day": false,
      "open_time": 3600,
      "close_time": 86400
    },
    {
      "id": "a7639d26-e5a9-49ba-a02a-f1462d6bb489",
      "wday": 3,
      "closed": false,
      "extra_day": false,
      "open_time": 3600,
      "close_time": 86400
    },
    {
      "id": "0e294591-277a-4157-84bf-dba428076ff3",
      "wday": 4,
      "closed": false,
      "extra_day": false,
      "open_time": 3600,
      "close_time": 86400
    },
    {
      "id": "740c4c28-e94c-4812-958f-a0ec3b7bc6fb",
      "wday": 5,
      "closed": false,
      "extra_day": false,
      "open_time": 3600,
      "close_time": 86400
    },
    {
      "id": "20970c7b-e366-4269-a17d-17c489395d12",
      "wday": 6,
      "closed": false,
      "extra_day": false,
      "open_time": 39600,
      "close_time": 86400
    }]
    }'
```

> If success, the above command returns status code 200

> if error, return 422 and following json object:

```json
{
  "errors": [
    "Sunday Open Time must be less than 86400",
    "Sunday Close Time must be greater than open time"
  ]
}
```

This endpoint authenticated by `Access Token`, and update establishment profile business hours

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`PATCH http://phrenzi.com/api/management/profile/business_hours`

### Query Parameters

Parameter | Description
--------- | -----------
business_hours | Array of Business Hour setting

## Update Billing Info

```shell
curl "https://phrenzi.com/api/management/profile/billing" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "establishment_name": "Awesome Bar",
    "token": "billing_token"
    }'
```

> if success, returns HTML status code 200 OK, with empty json

> if error, return HTML status code 422, with following json:

```json
{
  "errors": [
    "Token can't be blank"
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

This endpoint authenticated by `Access Token`, and update billing token for current establishment.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`PATCH http://phrenzi.com/api/management/profile/billing`

### Query Parameters

Parameter | Description
--------- | -----------
token | Billing token

## Accept Terms

```shell
curl "https://phrenzi.com/api/management/profile/terms" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -X PATCH
```

> if success, returns HTML status code 200 OK, with empty json

> if unauthorize, returns HTML status code 401, with following object:

``` json
{
  "errors": [
    "Authorized users only."
  ]
}
```

This endpoint authenticated by `Access Token`, and accept terms for current establishment.

### HTTP Request

`PATCH http://phrenzi.com/api/management/profile/terms`


## Location List

```shell
curl "https://phrenzi.com/api/management/profile/locations" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> if success, returns HTML status code 200 OK, with following json:

```json
{
  "locations": [
    {
      "id": "e3ff7a2f-cf0f-4c91-af56-2d2d3e9d3f20",
      "name": "location",
      "desc": "location desc",
      "lat": "1.2323",
      "long": "1.23333",
      "created_at": "2019-05-04T13:29:51Z",
      "updated_at": "2019-05-04T13:29:51Z"
    },
    {
      "id": "46bffe78-7049-443b-a27f-49da4689e9d7",
      "name": "location",
      "desc": "location desc",
      "lat": "2.2323",
      "long": "2.23333",
      "created_at": "2019-05-04T13:29:51Z",
      "updated_at": "2019-05-04T13:29:51Z"
    }
  ]
}
```

> if unauthorize, returns HTML status code 401, with following object:

``` json
{
  "errors": [
    "You need to sign in or sign up before continuing."
  ]
}
```

This endpoint authenticated by `Access Token`, and get locations list for current establishment.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`GET http://phrenzi.com/api/management/profile/locations`
