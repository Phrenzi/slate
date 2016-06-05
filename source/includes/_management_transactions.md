# Management / Transactions

## Get all transactions by establishment

```shell
curl "https://phrenzi.com/api/v1/management/transactions"
  -H "Authorization: manager_token"
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
    "patron_id": "ASSSFQWE",
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
    "patron_id": "ASSSFQWE",
    "type": "correct",
    "sale_amount": 0,
    "credit_amount": -20.00,
    "tracked_at": "2016-06-04T07:48:56.050Z"
  }
]
```

This endpoint authenticate by `manager_token`, and retrieves transaction records by establishment with different conditions.

### HTTP Request

`GET http://example.com/api/v1/management/transactions`

### Query Parameters

Parameter | Requred? | Description
--------- | ----------- | ---------
patron_id | N | if this patron_id is present, the result should only return transactions related to this
patron
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20

## Create Transaction
```shell
curl "https://phrenzi.com/api/v1/management/transactions"
  -H "Authorization: manager_token"
  -X POST
  -d '{
    "type": "sale",
    "sale_amount": 200.00
    }'
```

> The above command returns HTML status code 200 OK if success.

This endpoint required `manager_token`, and create transaction records.

### HTTP Request

`POST http://example.com/api/v1/management/transactions`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | -----------
type | Y | sale/correction
sale_amount | Y | the sale amount
credit_amount | N | the credit amount

### Query Exmaple:

normal sale record, without credit redeem:

Parameter | Description
--------- | -----------
type | 'sale'
sale_amount | 200.00

sale record, without partially credit redeem ( 200 sale amount, but with 125 credit redeem , so patron just need to pay 75.00 ):

Parameter | Description
--------- | -----------
type | 'sale'
sale_amount | 200.00
credit_amount | -125.00

sale record, fully credit redeem ( 200 sale amount, 200 credit redeem, so patron do not need to pay):

Parameter | Description
--------- | -----------
type | 'sale'
sale_amount | 200.00
credit_amount | -200.00

positive correction record:

Parameter | Description
--------- | -----------
type | 'correction'
sale_amount | 0.00
credit_amount | 125.00

negative correction record:

Parameter | Description
--------- | -----------
type | 'correction'
sale_amount | 0.00
credit_amount | -125.00
