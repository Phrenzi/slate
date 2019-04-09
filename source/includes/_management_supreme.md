# Management / Supreme / Establishment List

## Get all establishments list

```shell
curl "https://phrenzi.com/api/management/supreme/establishments" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token"
```

> The above command returns array of `Establishment` object like this:

```json
{
  "establishments": [
    {
      "id": "8d3d7ecd-585d-4f2f-ad21-1b457e062681",
      "name": "Awesome Bar"
    },
    {
      "id": "fcbdd18f-e5ea-4368-8cf4-2e688e604a40",
      "name": "Cafe Roma"
    }
  ]
}
```

This endpoint authenticated by `Access Token`, and manager need to be a super manager, this endpoint will retrieve all establishments.

### HTTP Request

`GET http://phrenzi.com/api/management/supreme/establishments`

## Select Establishment

```shell
curl "https://phrenzi.com/api/management/supreme/ddbd0c3c-404d-4ce1-9042-9baecb4ef585/select" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -X PATCH
```

> If success, The above command return status code 200 with empty json object

This endpoint authenticated by `Manger Token`, and manager need to be a super manager, this endpoint will update manager's establishment.

### HTTP Request

`PATCH http://phrenzi.com/api/management/supreme/ddbd0c3c-404d-4ce1-9042-9baecb4ef585/select`
