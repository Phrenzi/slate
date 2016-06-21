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
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X POST \
  -d '{
    "trans_type": "sale",
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
      "id": "4d585878-38ac-475a-8ed4-d1c837c82fc2",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "93257623-3acf-4c93-9051-91b19f88ca89",
        "trans-type": "sales",
        "sales-amount": "200.0",
        "credit-amount": "7.0",
        "status": "valid",
        "cash-back": "3.5",
        "trans-code": "37d298c26e",
        "group-code": null,
        "tracked-at": "2016-06-21T09:46:20.513Z",
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
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X POST \
  -d '{
    "trans_type": "sale",
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
      "id": "323020e0-daf6-4ce2-8e81-213b76cba704",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "fc8f34e3-2f48-4eb4-9253-9c6b16a2666d",
        "trans-type": "sales",
        "sales-amount": "75.0",
        "credit-amount": "2.63",
        "status": "valid",
        "cash-back": "3.5",
        "trans-code": "cf97cd3b95",
        "group-code": "7d3f193728",
        "tracked-at": "2016-06-21T09:49:00.313Z",
        "del-transaction-id": null
      }
    },
    {
      "id": "a4ad31ef-9d41-4fff-9b78-a954b4eef7d0",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "fc8f34e3-2f48-4eb4-9253-9c6b16a2666d",
        "trans-type": "credit",
        "sales-amount": "125.0",
        "credit-amount": "-125.0",
        "status": "valid",
        "cash-back": "3.5",
        "trans-code": "2d3a00a399",
        "group-code": "7d3f193728",
        "tracked-at": "2016-06-21T09:49:00.313Z",
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
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
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
      "id": "e55ee9ce-67d7-4e01-bd2d-3a7f81a817ca",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "42f1b39d-beae-4b5e-b8ec-ef0f5a92dac6",
        "trans-type": "credit",
        "sales-amount": "200.0",
        "credit-amount": "-200.0",
        "status": "valid",
        "cash-back": "3.5",
        "trans-code": "e32684cf06",
        "group-code": null,
        "tracked-at": "2016-06-21T09:51:37.922Z",
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
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
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
      "id": "5612adbc-9eec-4ece-8018-393b80b6bea1",
      "type": "transactions",
      "attributes": {
        "patron-id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
        "establishment-id": "f43fdfb3-19bd-4293-9678-e8e88a9bf0ba",
        "trans-type": "correction",
        "sales-amount": "0.0",
        "credit-amount": "-200.0",
        "status": "valid",
        "cash-back": "3.5",
        "trans-code": "19431b7947",
        "group-code": null,
        "tracked-at": "2016-06-21T09:54:05.348Z",
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
cash_back | N | cash back for one time use case
password | N | if cash_back is present, then password of patron must provided

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
