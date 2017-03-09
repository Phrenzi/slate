# PatronApp / Check In

## patron check in

```shell
curl "https://phrenzi.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/check_in" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X POST \
  -d '{
    "lat": "23.2333",
    "long": "-22.1234"
    }'
```

> The above command returns status code 200 with response of JSON structured like this:

```json
{
  "boosters": [ ]
}
```

> If patron's lat & long is closed enough to establishment, return status code 406 and following
> JSON response:

```json
{
  "errors": ["Current Location is not near enough"]
}
```

> If patron's lat & long have format error, return status code 422 and following JSON response:

```json
{
  "errors": { "lat": ["can't be blank"], "long": ["can't be blank"] }
}
```

This endpoint check in current logined patron into Establishment specify

### HTTP Request

`POST http://example.com/api/patron_app/establishments/:establishment_id/check_in`

### Query Parameters

NOTED: establishment_id is the uuid of establishment

Parameter | Required | Description
--------- | ----------- | -----------
lat | Y | latitude of patron's location, example '23.233'
long | Y | longitude of patron's location, example: '-23.233'
