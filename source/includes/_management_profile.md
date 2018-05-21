# Management / Profile

## Update Brand

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
  -H "Authorization: token" \
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

This endpoint authenticated by `Manager Token`, and update establishment profile logo or banner

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a>, and please make sure staff is a manager</aside>

### HTTP Request

`PATCH http://phrenzi.com/api/management/profile/images`

### Query Parameters

Parameter | Description
--------- | -----------
banner | Banner image
logo | Logo image
