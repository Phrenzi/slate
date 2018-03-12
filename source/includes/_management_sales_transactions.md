# Management / Sales Transactions

## Get all sales transactions by patron_id for current establishment

```shell
curl "https://phrenzi.com/api/management/sales_transactions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -d '{
    "patron_id": "a9ce92dd-1b1d-498a-b7d0-77fffccd20de"
    }'
```

> The above command returns JSON structured like this:

```json
{
  "transactions": [
    {
      "id": "15477325-11fa-4b85-87a9-30f6272656be",
      "patron_id": "a9ce92dd-1b1d-498a-b7d0-77fffccd20de",
      "establishment_id": "277e92b3-3332-4ccc-92e3-c17eb6e7c507",
      "challenge_id": null,
      "trans_type": "sales",
      "sales_amount": "100.0",
      "applied_credit": "0.0",
      "sales_credit": "3.5",
      "credit_subtotal": "3.5",
      "remaining_credit": "0.0",
      "cash_back": "3.5",
      "trans_code": "9a47366866",
      "group_code": null,
      "tracked_at": "2017-03-29T19:04:28.067+08:00",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false,
      "action": "Cash Purchase"
    },
    {
      "id": "0db22eca-326f-4b8c-b5bc-c517256cc64c",
      "patron_id": "a9ce92dd-1b1d-498a-b7d0-77fffccd20de",
      "establishment_id": "277e92b3-3332-4ccc-92e3-c17eb6e7c507",
      "challenge_id": null,
      "trans_type": "sales",
      "sales_amount": "100.0",
      "applied_credit": "0.0",
      "sales_credit": "3.5",
      "credit_subtotal": "3.5",
      "remaining_credit": "0.0",
      "cash_back": "3.5",
      "trans_code": "613ef86f6b",
      "group_code": null,
      "tracked_at": "2017-03-29T19:04:28.067+08:00",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false,
      "action": "Cash Purchase"
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and retrieves transaction records by establishment by patron

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### HTTP Request

`GET http://example.com/api/management/sales_transactions`

### Query Parameters

Parameter | Requred? | Description
--------- | ----------- | ---------
patron_id | N | only list transactions that belongs to patron
trans_code | N | transaction's trans_code
page | N | the page results of all transactions, default to be page 1
per_page | N | the number of transaction record return per page by api, default to be 20

## Create Sales Transaction

> For creating fullay sales transaction

```shell
curl "https://phrenzi.com/api/management/sales_transactions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
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
      "deleted": false,
      "action": "Cash Purchase"
    }
  ]
}
```

> For creating partially sales transaction

```shell
curl "https://phrenzi.com/api/management/sales_transactions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
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
      "deleted": false,
      "action": "Cash Purchase"
    },
    {
      "id": "441a3707-3015-4bb7-9df9-0d2fae3a4db1",
      "patron_id": "3afc8c7e-ea86-4b85-abb6-1a3616a80f6b",
      "establishment_id": "1ac3affe-540b-4fde-8dee-eb6ac5f38376",
      "challenge_id": null,
      "trans_type": "credit",
      "sales_amount": "125.0",
      "applied_credit": "-125.0",
      "sales_credit": "0.0",
      "credit_subtotal": "-120.6",
      "remaining_credit": "77.6",
      "cash_back": "3.5",
      "trans_code": "4042580c33",
      "group_code": "dc8225e705",
      "tracked_at": "2017-03-29T18:36:04.640+08:00",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false,
      "action": "Credit Purchase"
    }
  ]
}
```

> For creating fully credit redeem transaction

```shell
curl "https://phrenzi.com/api/management/sales_transactions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
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
      "sales_credit": "0.0",
      "credit_subtotal": "-200.0",
      "remaining_credit": "0.0",
      "cash_back": "3.5",
      "trans_code": "f1b1ef0e7b",
      "group_code": null,
      "tracked_at": "2017-03-29T18:39:44.563+08:00",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false,
      "action": "Credit Purchase"
    }
  ]
}
```

> For creating correction credit transaction

```shell
curl "https://phrenzi.com/api/management/sales_transactions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
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
      "deleted": false,
      "action": "Credit Correction"
    }
  ]
}
```

> Error Scenarios

```shell
curl "https://phrenzi.com/api/management/sales_transactions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
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
This endpoint authenticated by `Manager Token`, and create transaction records.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

### HTTP Request

`POST http://example.com/api/management/sales_transactions`

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

## Delete Sales Transaction

> For delete fullay sales transaction

```shell
curl "https://phrenzi.com/api/management/sales_transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X DELETE
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "transactions": [
    {
      "id": "f4ef1c91-105b-4323-b1cb-2642bb7fa870",
      "patron_id": "cce8f71d-5eda-4b74-b3ed-bc5fc46edfe3",
      "establishment_id": "d9b6a80d-309f-49d5-9714-39b80cef43f9",
      "challenge_id": null,
      "trans_type": "sales",
      "sales_amount": "-100.0",
      "applied_credit": "-0.0",
      "sales_credit": "-3.5",
      "credit_subtotal": "-3.5",
      "remaining_credit": "196.5",
      "cash_back": "3.5",
      "trans_code": "c57d322c62",
      "group_code": null,
      "tracked_at": "2017-03-29T18:51:41.470+08:00",
      "del_transaction_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "deleted_at": "2017-03-29T18:51:42.470+08:00",
      "deleted": true,
      "action": "Cash Purchase Deletion"
    }
  ]
}
```

> For delete partially sales transaction

```shell
curl "https://phrenzi.com/api/management/sales_transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X DELETE
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "transactions": [
    {
      "id": "e78701fa-259c-4608-83d8-ef8701841c07",
      "patron_id": "f0731af3-d5ce-4e75-a689-fdf13c05968f",
      "establishment_id": "5e1f01e1-d489-4d62-98d7-19a4d21345cc",
      "challenge_id": null,
      "trans_type": "sales",
      "sales_amount": "-75.0",
      "applied_credit": "-0.0",
      "sales_credit": "-2.63",
      "credit_subtotal": "-2.63",
      "remaining_credit": "197.37",
      "cash_back": "3.5",
      "trans_code": "902c2747aa",
      "group_code": "abcdefgfhi",
      "tracked_at": "2017-03-29T18:53:10.256+08:00",
      "del_transaction_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "deleted_at": "2017-03-29T18:53:12.256+08:00",
      "deleted": true,
      "action": "Cash Purchase Deletion"
    },
    {
      "id": "41c6f8d1-6539-436e-aeef-86d870c7f4c1",
      "patron_id": "f0731af3-d5ce-4e75-a689-fdf13c05968f",
      "establishment_id": "5e1f01e1-d489-4d62-98d7-19a4d21345cc",
      "challenge_id": null,
      "trans_type": "credit",
      "sales_amount": "-125.0",
      "applied_credit": "125.0",
      "sales_credit": "-0.0",
      "credit_subtotal": "125.0",
      "remaining_credit": "322.37",
      "cash_back": "3.5",
      "trans_code": "5fc5031cc8",
      "group_code": "abcdefgfhi",
      "tracked_at": "2017-03-29T18:53:11.256+08:00",
      "del_transaction_id": "6a2c4670-c588-401a-9f03-a9c8783557be",
      "deleted_at": "2017-03-29T18:53:12.256+08:00",
      "deleted": true,
      "action": "Credit Purchase Deletion"
    }
  ]
}
```

> For delete fully credit redeem transaction

```shell
curl "https://phrenzi.com/api/management/sales_transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X DELETE
```

> The above command returns HTML status code 200 OK if success and json object

``` json
{
  "transactions": [
    {
      "id": "11408bea-bb4d-460d-8614-9ca74e5419bf",
      "patron_id": "51b5e8fe-7724-45a7-a118-9eef4d6196cd",
      "establishment_id": "5ca16c11-5f5e-4fda-ae6f-b485161710ed",
      "challenge_id": null,
      "trans_type": "credit",
      "sales_amount": "-200.0",
      "applied_credit": "200.0",
      "sales_credit": "-0.0",
      "credit_subtotal": "200.0",
      "remaining_credit": "400.0",
      "cash_back": "3.5",
      "trans_code": "12d7967d6e",
      "group_code": null,
      "tracked_at": "2017-03-29T18:55:17.344+08:00",
      "del_transaction_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "deleted_at": "2017-03-29T18:55:18.344+08:00",
      "deleted": true,
      "action": "Credit Purchase Deletion"
    }
  ]
}
```

> While specify delete transaction is invalid, or fake, or not belongs to current establishment

```shell
curl "https://phrenzi.com/api/management/sales_transactions/this-is-a-fake-id" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
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

> While specify delete transaction is created 30 days before,

```shell
curl "https://phrenzi.com/api/management/sales_transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X DELETE
```

> The above command returns HTML status code 406 and following json object

``` json
{
  "errors": [
    "Can not delete transaction created 30 days before"
  ]
}
```

This endpoint authenticated by `Manager Token`, and delete transaction records.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

### HTTP Request

`DELETE http://example.com/api/management/sales_transactions/#{transaction_id}`
