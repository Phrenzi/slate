# Patron / Transactions

## get all transactions for patron

```shell
curl "https://phrenzi.com/api/v1/patrons/transactions"
  -H "Authorization: user_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "WE7EASD",
    "patron_id": "ASDFQWE",
    "type": "sale",
    "sale_amount": 75.00,
    "credit_amount": 2.63,
    "tracked_at": "2016-06-04T07:48:56.050Z"
  },
  {
    "id": "WE7EASS",
    "patron_id": "ASDFQWE",
    "type": "credit",
    "sale_amount": 125.00,
    "credit_amount": -125.00,
    "tracked_at": "2016-06-04T07:48:56.050Z"
  },
  {
    "id": "WE7EASE",
    "patron_id": "ASDFQWE",
    "type": "correct",
    "sale_amount": 0,
    "credit_amount": 2.00,
    "tracked_at": "2016-06-04T07:48:56.050Z"
  },
  {
    "id": "WE7ESSE",
    "patron_id": "ASDFQWE",
    "type": "correct",
    "sale_amount": 0,
    "credit_amount": -20.00,
    "tracked_at": "2016-06-04T07:48:56.050Z"
  }
]
```

This endpoint authenticate by `user_token`, and retrieves all transaction for specific user

### HTTP Request

`GET http://example.com/api/v1/patrons/establishments`

### Query Parameters

Parameter | Description
--------- | -----------
page | the page results of all transactions
per_page | the number of transaction record return per page by api, default to be 20
