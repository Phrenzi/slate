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
      "challenge_id": null,
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
      "challenge_id": null,
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
      "id": "1f485151-80ad-4d25-88bd-89e343b1e7f6",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "3da90d84-92db-487f-af45-e020fbcaf0bd",
      "challenge_id": null,
      "trans_type": "sales",
      "sales_amount": "200.0",
      "applied_credit": "0.0",
      "sales_credit": "7.0",
      "credit_subtotal": "7.0",
      "remaining_credit": "7.0",
      "cash_back": "3.5",
      "trans_code": "9914f6658f",
      "group_code": null,
      "tracked_at": "2017-03-29T18:33:58.327+08:00",
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
    "patron_id": "3afc8c7e-ea86-4b85-abb6-1a3616a80f6b",
    "sales_amount": 200.00,
    "credit_amount": -125.0
    }'
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "transactions": [
    {
      "id": "1f1ba450-4e4c-4570-bf4f-26cf6664566b",
      "patron_id": "3afc8c7e-ea86-4b85-abb6-1a3616a80f6b",
      "establishment_id": "1ac3affe-540b-4fde-8dee-eb6ac5f38376",
      "challenge_id": null,
      "trans_type": "sales",
      "sales_amount": "75.0",
      "applied_credit": "0.0",
      "sales_credit": "2.6",
      "credit_subtotal": "2.6",
      "remaining_credit": "202.6",
      "cash_back": "3.5",
      "trans_code": "2fdbce4d14",
      "group_code": "dc8225e705",
      "tracked_at": "2017-03-29T18:36:04.640+08:00",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    },
    {
      "id": "441a3707-3015-4bb7-9df9-0d2fae3a4db1",
      "patron_id": "3afc8c7e-ea86-4b85-abb6-1a3616a80f6b",
      "establishment_id": "1ac3affe-540b-4fde-8dee-eb6ac5f38376",
      "challenge_id": null,
      "trans_type": "credit",
      "sales_amount": "125.0",
      "applied_credit": "-125.0",
      "sales_credit": "4.4",
      "credit_subtotal": "-120.6",
      "remaining_credit": "82.0",
      "cash_back": "3.5",
      "trans_code": "4042580c33",
      "group_code": "dc8225e705",
      "tracked_at": "2017-03-29T18:36:04.640+08:00",
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
      "id": "4f27f679-af58-4046-8b96-49f53148f8b4",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "95884702-f53a-4bec-891b-ec9b0bbb5acb",
      "challenge_id": null,
      "trans_type": "credit",
      "sales_amount": "200.0",
      "applied_credit": "-200.0",
      "sales_credit": "7.0",
      "credit_subtotal": "-193.0",
      "remaining_credit": "7.0",
      "cash_back": "3.5",
      "trans_code": "f1b1ef0e7b",
      "group_code": null,
      "tracked_at": "2017-03-29T18:39:44.563+08:00",
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
      "id": "b4c6b6c6-7bca-47f9-97ea-e470480a4475",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "f9a3eed7-b948-4ad9-bf09-b8a54807ccab",
      "challenge_id": null,
      "trans_type": "correction",
      "sales_amount": "0.0",
      "applied_credit": "0.0",
      "sales_credit": "0.0",
      "credit_subtotal": "-200.0",
      "remaining_credit": "0.0",
      "cash_back": "0.0",
      "trans_code": "25aa44f431",
      "group_code": null,
      "tracked_at": "2017-03-29T18:40:32.878+08:00",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    }
  ]
}
```

> Error Scenarios

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

> if establishment is not open, the above command returns status code 406, and errors json like this:

```json
{
  "errors": ["Current Establishment is not opened"]
}
```

> if current credit balance is not enough, then return status code 406, and errors json like this:

```json
{
  "errors": ["Balance not enough"]
}
```

> if input validation is failed

```json
{
  "errors": {
    "trans_type": ["is not included in the list"]
  }
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
      "challenge_id": null,
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
      "challenge_id": null,
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
      "challenge_id": null,
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
      "challenge_id": null,
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
      "challenge_id": null,
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
