# Management / Transactions

## Get all transactions by patron_id for current establishment

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
      "cash_back": "3.5",
      "trans_code": "621f3849e5",
      "group_code": null,
      "tracked_at": "2016-06-26T13:22:17.005Z",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    },
    {
      "id": "4e47edfd-fd56-4ceb-ba12-b9e233da8436",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "e405f87e-447b-4308-a39f-1e6505ba5503",
      "trans_type": "sales",
      "sales_amount": "100.0",
      "credit_amount": "3.5",
      "cash_back": "3.5",
      "trans_code": "c76f93d48b",
      "group_code": null,
      "tracked_at": "2016-06-26T13:22:17.005Z",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
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
      "cash_back": "3.5",
      "trans_code": "5305ec72be",
      "group_code": null,
      "tracked_at": "2016-06-26T13:14:38.953Z",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
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
      "cash_back": "3.5",
      "trans_code": "b9dd87d694",
      "group_code": "ff84acbaaf",
      "tracked_at": "2016-06-26T13:16:04.090Z",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    },
    {
      "id": "b9321494-9096-479d-ad74-2c00f1762ac2",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "86aef2ae-3651-4dad-90ad-303a8f476638",
      "trans_type": "credit",
      "sales_amount": "125.0",
      "credit_amount": "-125.0",
      "cash_back": "3.5",
      "trans_code": "9afa1212a9",
      "group_code": "ff84acbaaf",
      "tracked_at": "2016-06-26T13:16:04.090Z",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
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
      "cash_back": "3.5",
      "trans_code": "41c7eed125",
      "group_code": null,
      "tracked_at": "2016-06-26T13:17:46.515Z",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
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
      "cash_back": "3.5",
      "trans_code": "1a3f96b921",
      "group_code": null,
      "tracked_at": "2016-06-26T13:18:36.521Z",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
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

## Delete Transaction

> For delete fullay sales transaction

```shell
curl "https://phrenzi.com/api/management/transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X DELETE
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "transactions": [
    {
      "id": "3cf13c1d-a1b8-4258-9ae0-4239cd5c81df",
      "patron_id": "c801514d-8063-4a79-82cc-686747165a85",
      "establishment_id": "af84f935-9ab5-41f9-abe5-37a06a6dfa36",
      "trans_type": "sales",
      "sales_amount": "-100.0",
      "credit_amount": "-3.5",
      "cash_back": "3.5",
      "trans_code": "362b2882f2",
      "group_code": null,
      "tracked_at": "2016-06-26T13:36:32.563Z",
      "del_transaction_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "deleted_at": "2016-06-27T13:36:32.563Z",
      "deleted": true,
    }
  ]
}
```

> For delete partially sales transaction

```shell
curl "https://phrenzi.com/api/management/transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X DELETE
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "transactions": [
    {
      "id": "db2a88e1-072b-42ef-a9b9-0af3cd2977ac",
      "patron_id": "42d7d7c1-c8f6-4444-9472-a34322c091a9",
      "establishment_id": "24b0345f-d06b-4fed-b1c6-50bd424028b0",
      "trans_type": "sales",
      "sales_amount": "-75.0",
      "credit_amount": "-2.63",
      "cash_back": "3.5",
      "trans_code": "60c1bb42e9",
      "group_code": "abcdefgfhi",
      "tracked_at": "2016-06-26T13:39:07.321Z",
      "del_transaction_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "deleted_at": "2016-06-27T13:36:32.563Z",
      "deleted": true,
    },
    {
      "id": "adc33168-1207-4370-9852-da6563a890a5",
      "patron_id": "42d7d7c1-c8f6-4444-9472-a34322c091a9",
      "establishment_id": "24b0345f-d06b-4fed-b1c6-50bd424028b0",
      "trans_type": "credit",
      "sales_amount": "-125.0",
      "credit_amount": "125.0",
      "cash_back": "3.5",
      "trans_code": "3285af74bb",
      "group_code": "abcdefgfhi",
      "tracked_at": "2016-06-26T13:39:07.321Z",
      "del_transaction_id": "6a7b9c7f-f32e-4a9f-905e-057cd4acd9cb",
      "deleted_at": "2016-06-27T13:36:32.563Z",
      "deleted": true,
    }
  ]
}
```

> For delete fully credit redeem transaction

```shell
curl "https://phrenzi.com/api/management/transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X DELETE
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "transactions": [
    {
      "id": "2f8cb908-2997-417a-941c-9ccb15da0a29",
      "patron_id": "b4e18a28-9ccc-4e47-bd34-3241998410b1",
      "establishment_id": "744275ee-714d-40eb-8657-880725bbeb9b",
      "trans_type": "credit",
      "sales_amount": "-200.0",
      "credit_amount": "200.0",
      "cash_back": "3.5",
      "trans_code": "6e2dd918c6",
      "group_code": null,
      "tracked_at": "2016-06-26T13:41:33.685Z",
      "del_transaction_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "deleted_at": "2016-06-27T13:36:32.563Z",
      "deleted": true,
    }
  ]
}
```

> For delete correction credit transaction


```shell
curl "https://phrenzi.com/api/management/transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X DELETE
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "transactions": [
    {
      "id": "10d1a032-ca48-4d08-b078-5c74e76fb6cc",
      "patron_id": "a540cb87-a662-4b89-b1f0-47e4c62eb3c2",
      "establishment_id": "4020f704-6ea8-4323-85bf-0a5d9b04140a",
      "trans_type": "correction",
      "sales_amount": "-0.0",
      "credit_amount": "-200.0",
      "cash_back": "3.5",
      "trans_code": "eb7b042ac2",
      "group_code": null,
      "tracked_at": "2016-06-26T13:42:53.904Z",
      "del_transaction_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "deleted_at": "2016-06-27T13:36:32.563Z",
      "deleted": true,
    }
  ]
}
```

> While specify delete transaction is invalid, or fake, or not belongs to current establishment

```shell
curl "https://phrenzi.com/api/management/transactions/this-is-a-fake-id" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X DELETE
```

> The above command returns HTML status code 406 and following json object

``` json
{
  "errors": [
    "Transaction is invalid"
  ]
}
```

This endpoint required manager authentication, and delete transaction records.

### HTTP Request

`DELETE http://example.com/api/management/transactions/#{transaction_id}`
