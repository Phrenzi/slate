# PatronApp / Profile Image

## pre-sign url

```shell
curl "https://phrenzi.com/api/patron_app/patron_profile/cache/presign" \
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

`GET http://example.com/api/patron_app/patron_profiile/cache/presign`

After you retrive the presign url, you could be able to make a post request to presign url with the fields this end-point provided. Then you could be able to retrieve an id from S3. Please construct a json object with this id, and this object will going to be used in next API call to create the actual profile image in Phrenzi

For more detail, please visit shrine's plugin [direct_upload](http://shrinerb.com/rdoc/files/doc/direct_s3_md.html)

## create patron profile

```shell
curl "https://phrenzi.com/api/patron_app/profile" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X POST \
  -d '{
        "profile": '{
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

> The above command returns status code 200

### HTTP Request

`POST http://example.com/api/patron_app/profile`


### URL Parameters
Parameter | Description
--------- | -----------
profile | String, json object string demonstrated above

NOTED: id & storage is required in json object string

For full scenario of upload profile with pre-sign, please refer
[here](https://github.com/Phrenzi/phrenzi_web/blob/master/spec/requests/api/v1/patron_app/patron_profile_spec.rb)

## update patron profile

```shell
curl "https://phrenzi.com/api/patron_app/profile" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token" \
  -X PATCH \
  -d '{
        "profile": '{
          "id": "349234854924394", # required
          "storage": "cache", # required
          "metadata": {
            "size": 45461, # optional
            "filename": "foo.jpg", # optional
            "mime_type": "image/jpeg", # optional
          }
        }',
        "name": "Simon",
        "email": "manin.iong@gmail.com",
        "reconfirm_success_url": "phrenzi://"
      }'
```

> The above command returns status code 200

### HTTP Request

`PATCH http://example.com/api/patron_app/profile`

### URL Parameters
Parameter | Description
--------- | -----------
profile | String, json object string demonstrated above
name | String, name of current login Patron
email | String, new email of current login Patron
reconfirm_success_url | after new email is confirmed, specify the url to redirect to, if email is present, reconfirm_success_url must be present.

NOTED:

1. for `profile` json object, `id` & `storage` is required in json object string
2. `profile`, `name`, `email` must have at least one present in the payload.

For full scenario of upload profile with pre-sign, please refer
[here](https://github.com/Phrenzi/phrenzi_web/blob/master/spec/requests/api/v1/patron_app/patron_profile_spec.rb)

### The flow for update email

1. current patron call update profile api, with `email` & `reconfirm_success_url` payload.
2. server return success, and at the same time, send a confirmatino email to new email inbox
3. At this time being, patron is still authenticated ( not force logout ), patron can still login using old email
4. Patron go to new email inbox, click the click there, this will trigger a confirmation request in the server, and patron will redirect to the url specify in `reconfirm_success_url` payload.
5. At this time being, patron can not login using old email but the new one.
