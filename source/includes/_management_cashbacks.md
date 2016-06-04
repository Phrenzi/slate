# Management / Cashback

## Get cash back

```shell
curl "https://phrenzi.com/api/v1/management/cash_back"
  -H "Authorization: your_token"
```

> The above command returns JSON structured like this:

```json
{
  "cash_back": 3.5
}
```

This endpoint require manager token, and current cash_back for current establishment.

### HTTP Request

`GET http://phrenzi.com/api/v1/management/cash_back`

## Update cash back

```shell
curl "https://phrenzi.com/api/v1/management/cash_back"
  -H "Authorization: your_token"
  -X PATCH
  -d '{
    "cash_back": 4.5
    }'
```

> The above command returns HTML status code 200 OK

This endpoint require manager token, and update cash_back for current establishment.

### HTTP Request

`PATCH http://phrenzi.com/api/v1/management/cash_back`

### Query Parameters

Parameter | Description
--------- | -----------
cash_back | the cash_back to update, within 0 and 100
