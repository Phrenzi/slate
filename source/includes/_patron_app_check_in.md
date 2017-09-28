# PatronApp / Check In

## patron check in

```shell
curl "https://phrenzi.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/check_in" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X POST \
  -d '{
    "lat": "23.2333",
    "long": "-22.1234"
    }'
```

> The above command returns status code 200 with response of JSON structured like this:

```json
{
  "boosters": [
    {
      "id": "202f96fb-1536-43fa-a6ba-7b0387e90465",
      "type": "check_in",
      "status": "failed",
      "error_code": "REDEEMED_ALREADY"
    },
    {
      "id": "40be79a4-92b3-447a-aff2-0ab5f9210aca",
      "type": "check_in",
      "status": "failed",
      "error_code": "REACH_REDEEM_COUNT"
    },
    {
      "id": "c3c7fdf5-8629-4c13-9b86-b911ab86adce",
      "type": "check_in",
      "status": "failed",
      "error_code": "EXPIRED"
    },
    {
      "id": "39c42912-91cf-48dd-abbf-a273da146568",
      "type": "check_in",
      "status": "success",
      "point": "100.0"
    },
    {
      "id": "39c42912-91cf-48dd-abbf-b911ab86adce",
      "type": "invitation",
      "status": "success",
      "point": "0.0"
    },
    {
      "id": "c3c7fdf5-91cf-48dd-abbf-b911ab86adce",
      "type": "invitation",
      "status": "success",
      "point": "200.0"
    },
    {
      "id": "c3c7fdf5-91cf-48dd-abbf-b911ab86adce",
      "type": "invitation",
      "status": "failed",
      "error_code": "CHECKED_IN"
    }
  ]
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

> If current there's no challenge today, return status code 406 and following JSON response:

```json
{
  "errors": ["There is no active Challenge today"]
}
```

This endpoint authenticated by `Patron Token` and check in current logined patron into Establishment specify

### HTTP Request

`POST http://example.com/api/patron_app/establishments/:establishment_id/check_in`

### Query Parameters

NOTED: establishment_id is the uuid of establishment

Parameter | Required | Description
--------- | ----------- | -----------
lat | Y | latitude of patron's location, example '23.233'
long | Y | longitude of patron's location, example: '-23.233'
