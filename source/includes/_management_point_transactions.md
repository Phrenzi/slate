# Management / Point Transactions

## Get all transactions for current establishment

```shell
curl "https://phrenzi.com/api/management/point_transactions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -d '{
    "patron_id": "602247e3-9a20-4862-b772-a7fd617fc227"
    }'
```

> The above command returns JSON structured like this:

```json
{
  "transactions": [
    {
      "id": "7883337f-2353-4195-ae45-c8c554a916f5",
      "patron_id": "602247e3-9a20-4862-b772-a7fd617fc227",
      "establishment_id": "5f4c1f46-0e9b-4526-9bdf-1f85ba7f2869",
      "challenge_id": "7417f876-a72f-490c-9324-f4b81003cbf3",
      "point": 9,
      "action": "Purchase Points",
      "trans_code": "9993bad9ec",
      "tracked_at": "2018-03-05T13:39:03Z",
      "correction": false,
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    },
    {
      "id": "61227894-84f1-452d-8c4f-d5979f607097",
      "patron_id": "602247e3-9a20-4862-b772-a7fd617fc227",
      "establishment_id": "5f4c1f46-0e9b-4526-9bdf-1f85ba7f2869",
      "challenge_id": "7417f876-a72f-490c-9324-f4b81003cbf3",
      "point": 9,
      "action": "Purchase Points",
      "trans_code": "aa5c8f5c95",
      "tracked_at": "2018-03-05T13:39:02Z",
      "correction": false,
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and retrieves point transaction records by establishment by patron

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### HTTP Request

`GET http://example.com/api/management/point_transactions`

### Query Parameters

Parameter | Requred? | Description
--------- | ----------- | ---------
patron_id | N | only list transactions that belongs to patron
page | N | the page results of all transactions, default to be page 1
per_page | N | the number of transaction record return per page by api, default to be 20

## Delete Point Transaction

> For delete task redeemed point transaction

```shell
curl "https://phrenzi.com/api/management/point_transactions/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
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
      "id": "008b511b-5d68-454f-9112-619ca2d703ae",
      "patron_id": "fa2b6e2e-4a61-4254-938b-d00e1114c668",
      "establishment_id": "ad4f2664-e0ac-4450-aa54-4ff4b1986411",
      "challenge_id": "e8ad41d9-b98a-4003-b375-ec61b6204a4a",
      "point": -9,
      "action": "Task Booster Deletion",
      "trans_code": "88711d07e0",
      "tracked_at": "2018-03-12T07:15:58Z",
      "correction": false,
      "del_transaction_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "deleted_at": "2018-03-12T07:15:58Z",
      "deleted": true
    }
  ]
}
```

> While specify delete transaction is invalid, or not belongs to current establishment

```shell
curl "https://phrenzi.com/api/management/point_transactions/this-is-a-fake-id" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X DELETE
```

> The above command returns HTML status code 406 and following json object

``` json
{
  "errors": [
    "Point Transaction is invalid"
  ]
}
```


This endpoint authenticated by `Manager Token`, and delete point transaction records.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

### HTTP Request

`DELETE http://example.com/api/management/point_transactions/#{transaction_id}`
