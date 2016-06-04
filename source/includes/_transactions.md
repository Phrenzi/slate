# Transactions

## get all transactions

```shell
curl "https://phrenzi.com/api/v1/transactions"
  -H "Authorization: your_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "WE7EASD",
    "type": "sale",
    "sale_amount": 75.00,
    "credit_amount": 2.63,
    "track_at": "2016-06-04T07:48:56.050Z"
  },
  {
    "id": "WE7EASS",
    "type": "credit",
    "sale_amount": 125.00,
    "credit_amount": -125.00,
    "track_at": "2016-06-04T07:48:56.050Z"
  },
  {
    "id": "WE7EASE",
    "type": "correct",
    "sale_amount": 0,
    "credit_amount": 2.00,
    "track_at": "2016-06-04T07:48:56.050Z"
  },
  {
    "id": "WE7ESSE",
    "type": "correct",
    "sale_amount": 0,
    "credit_amount": -20.00,
    "track_at": "2016-06-04T07:48:56.050Z"
  }
]
```

This endpoint required user authenticate, and retrieves all transaction for specific user

### HTTP Request

`GET http://example.com/api/v1/establishments`

### Query Parameters

Parameter | Description
--------- | -----------
page | the page results of all transactions
per_page | the number of transaction record return per page by api, default to be 20
