# Management / Transactions

## Get all transactions by establishment

```shell
curl "https://phrenzi.com/api/management/transactions" \
  -H "Content-Type: application/json" \
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

`GET http://example.com/api/management/transactions`

### Query Parameters

Parameter | Requred? | Description
--------- | ----------- | ---------
patron_id | N | if this patron_id is present, the result should only return transactions related to this
patron
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20

## Create Transaction

> For creating fullay sales transaction

```shell
curl "https://phrenzi.com/api/management/transactions" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{
    "type": "sale",
    "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
    "sales_amount": 200.00,
    "credit_amount": 0.0
    }'
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "data": [
    {
      "id": "a631d16e-4b44-46e8-9009-164968c7830f",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "7e3d405d-d3d4-4afe-90bd-13e06bfc5a1c",
        "trans-type": "sales",
        "sales-amount": "200.0",
        "credit-amount": "7.0",
        "status": "valid",
        "cash-back": "3.5",
        "tracked-at": "2016-06-20T15:08:33.304Z",
        "ref-transaction-id": null,
        "del-transaction-id": null
      }
    }
  ]
}
```

> For creating partially sales transaction

```shell
curl "https://phrenzi.com/api/management/transactions" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{
    "type": "sale",
    "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
    "sales_amount": 200.00,
    "credit_amount": -125.0
    }'
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "data": [
    {
      "id": "9a6d5acb-e40f-4692-b632-65c75df18e8c",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "082d6018-a787-4d68-9cf3-93273a93c31a",
        "trans-type": "sales",
        "sales-amount": "75.0",
        "credit-amount": "2.63",
        "status": "valid",
        "cash-back": "3.5",
        "tracked-at": "2016-06-20T15:10:28.481Z",
        "ref-transaction-id": null,
        "del-transaction-id": null
      }
    },
    {
      "id": "62d57e1c-f243-4fae-9c93-41abfd3acdeb",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "082d6018-a787-4d68-9cf3-93273a93c31a",
        "trans-type": "credit",
        "sales-amount": "125.0",
        "credit-amount": "-125.0",
        "status": "valid",
        "cash-back": "3.5",
        "tracked-at": "2016-06-20T15:10:28.481Z",
        "ref-transaction-id": "9a6d5acb-e40f-4692-b632-65c75df18e8c",
        "del-transaction-id": null
      }
    }
  ]
}
```

> For creating fully credit redeem transaction

```shell
curl "https://phrenzi.com/api/management/transactions" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{
    "type": "sale",
    "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
    "sales_amount": 200.00,
    "credit_amount": -200.0
    }'
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "data": [
    {
      "id": "45a9a86e-0bf4-4b2c-a7ef-8c4f2f6c31d9",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "3ba82033-53a2-4ec1-9755-3267d29e66c9",
        "trans-type": "credit",
        "sales-amount": "200.0",
        "credit-amount": "-200.0",
        "status": "valid",
        "cash-back": "3.5",
        "tracked-at": "2016-06-20T15:12:22.047Z",
        "ref-transaction-id": null,
        "del-transaction-id": null
      }
    }
  ]
}
```

> For creating correction credit transaction

```shell
curl "https://phrenzi.com/api/management/transactions" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{
    "type": "correction",
    "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
    "sales_amount": 0.0,
    "credit_amount": -200.0
    }'
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "data": [
    {
      "id": "acbd64f2-3cba-491a-ac71-55fbd3f04f50",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "983a26d0-fbc5-4fcc-9c8c-2920b0501bad",
        "trans-type": "correction",
        "sales-amount": "0.0",
        "credit-amount": "-200.0",
        "status": "valid",
        "cash-back": "3.5",
        "tracked-at": "2016-06-20T15:13:48.885Z",
        "ref-transaction-id": null,
        "del-transaction-id": null
      }
    }
  ]
}
```

This endpoint required manager authentication, and create transaction records.

### HTTP Request

`POST http://example.com/api/management/transactions`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | -----------
trans_type | Y | 'sales'/'correction'
sales_amount | Y | the sale amount
credit_amount | Y | the credit amount
patron_id | Y | UUID of patron

### Query Exmaple:

normal sale record, without credit redeem:

Parameter | Description
--------- | -----------
trans_type | 'sale'
patron_id | "ddbd0c3c-404d-4ce1-9042-9baecb4ef585"
sales_amount | 200.0
credit_amount | 0.0

sale record, with partially credit redeem ( 200 sale amount, but with 125 credit redeem , so patron just need to pay 75.0 ):

Parameter | Description
--------- | -----------
trans_type | 'sale'
patron_id | "ddbd0c3c-404d-4ce1-9042-9baecb4ef585"
sales_amount | 200.0
credit_amount | -125.0

sale record, fully credit redeem ( 200 sale amount, 200 credit redeem, so patron do not need to pay):

Parameter | Description
--------- | -----------
trans_type | 'sale'
patron_id | "ddbd0c3c-404d-4ce1-9042-9baecb4ef585"
sales_amount | 200.0
credit_amount | -200.0

positive correction record:

Parameter | Description
--------- | -----------
trans_type | 'correction'
patron_id | "ddbd0c3c-404d-4ce1-9042-9baecb4ef585"
sales_amount | 0.0
credit_amount | 125.0

negative correction record:

Parameter | Description
--------- | -----------
trans_type | 'correction'
patron_id | "ddbd0c3c-404d-4ce1-9042-9baecb4ef585"
sales_amount | 0.0
credit_amount | -125.0
