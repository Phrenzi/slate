# Management / Transactions

## Get all transactions by establishment

```shell
curl "https://phrenzi.com/api/management/transactions" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -d '{
    "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585"
    }'
```

> The above command returns JSON structured like this:

```json
{
  "transactions": [
    {
      "id": "bf77e8f9-c01d-4dc1-9fba-d79427f1cd8e",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "e405f87e-447b-4308-a39f-1e6505ba5503",
      "trans_type": "sales",
      "sales_amount": "100.0",
      "credit_amount": "3.5",
      "status": "valid",
      "cash_back": "3.5",
      "trans_code": "621f3849e5",
      "group_code": null,
      "tracked_at": "2016-06-26T13:22:17.005Z",
      "del_transaction_id": null
    },
    {
      "id": "4e47edfd-fd56-4ceb-ba12-b9e233da8436",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "e405f87e-447b-4308-a39f-1e6505ba5503",
      "trans_type": "sales",
      "sales_amount": "100.0",
      "credit_amount": "3.5",
      "status": "valid",
      "cash_back": "3.5",
      "trans_code": "c76f93d48b",
      "group_code": null,
      "tracked_at": "2016-06-26T13:22:17.005Z",
      "del_transaction_id": null
    }
  ],
  "meta": {
    "current_page": 1,
    "next_page": null,
    "prev_page": null,
    "total_pages": 1,
    "total_count": 2
  }
}
```

This endpoint need manager authentication, and retrieves transaction records by establishment by patron

### HTTP Request

`GET http://example.com/api/management/transactions`

### Query Parameters

Parameter | Requred? | Description
--------- | ----------- | ---------
patron_id | Y | only list transactions that belongs to patron
page | N | the page results of all transactions, default to be page 1
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
  "transactions": [
    {
      "id": "fc3dc0d4-5500-4727-a817-b63e92b8303d",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "baa7bd5c-2daf-44b4-8abb-9918b2001ca3",
      "trans_type": "sales",
      "sales_amount": "200.0",
      "credit_amount": "7.0",
      "status": "valid",
      "cash_back": "3.5",
      "trans_code": "5305ec72be",
      "group_code": null,
      "tracked_at": "2016-06-26T13:14:38.953Z",
      "del_transaction_id": null
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
  "transactions": [
    {
      "id": "67c622ae-8048-4ccb-983c-a5e467b8d1ba",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "86aef2ae-3651-4dad-90ad-303a8f476638",
      "trans_type": "sales",
      "sales_amount": "75.0",
      "credit_amount": "2.63",
      "status": "valid",
      "cash_back": "3.5",
      "trans_code": "b9dd87d694",
      "group_code": "ff84acbaaf",
      "tracked_at": "2016-06-26T13:16:04.090Z",
      "del_transaction_id": null
    },
    {
      "id": "b9321494-9096-479d-ad74-2c00f1762ac2",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "86aef2ae-3651-4dad-90ad-303a8f476638",
      "trans_type": "credit",
      "sales_amount": "125.0",
      "credit_amount": "-125.0",
      "status": "valid",
      "cash_back": "3.5",
      "trans_code": "9afa1212a9",
      "group_code": "ff84acbaaf",
      "tracked_at": "2016-06-26T13:16:04.090Z",
      "del_transaction_id": null
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
  "transactions": [
    {
      "id": "a2b26425-90da-4273-a57a-a8f5a0d4981a",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "c01057e7-6e17-4395-9230-eb5204a6dd5a",
      "trans_type": "credit",
      "sales_amount": "200.0",
      "credit_amount": "-200.0",
      "status": "valid",
      "cash_back": "3.5",
      "trans_code": "41c7eed125",
      "group_code": null,
      "tracked_at": "2016-06-26T13:17:46.515Z",
      "del_transaction_id": null
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
  "transactions": [
    {
      "id": "371051f9-0214-4ff3-bc82-6cea5b96f9f8",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "a4999183-fa78-4191-8402-1538eb747c23",
      "trans_type": "correction",
      "sales_amount": "0.0",
      "credit_amount": "-200.0",
      "status": "valid",
      "cash_back": "3.5",
      "trans_code": "1a3f96b921",
      "group_code": null,
      "tracked_at": "2016-06-26T13:18:36.521Z",
      "del_transaction_id": null
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
