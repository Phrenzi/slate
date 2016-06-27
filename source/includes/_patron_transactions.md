# PatronApp / Transactions

## get all transactions by establishment_id

```shell
curl "https://phrenzi.com/api/patron_app/transactions" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -d '{
    "establishment_id": "a66d32c1-b50b-427e-8954-ec945e402f6d"
    }'
```

> The above command returns JSON structured like this:

```json
{
  "transactions": [
    {
      "id": "b80221a1-3f91-4979-b14f-f6d477b90561",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "a66d32c1-b50b-427e-8954-ec945e402f6d",
      "trans_type": "sales",
      "sales_amount": "100.0",
      "credit_amount": "3.5",
      "cash_back": "3.5",
      "trans_code": "62ada2ca5e",
      "group_code": null,
      "tracked_at": "2016-06-27T13:38:55.455Z",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    },
    {
      "id": "a494ed0a-d7f9-4f6a-8dec-3ccc05fddc5e",
      "patron_id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
      "establishment_id": "a66d32c1-b50b-427e-8954-ec945e402f6d",
      "trans_type": "sales",
      "sales_amount": "100.0",
      "credit_amount": "3.5",
      "cash_back": "3.5",
      "trans_code": "f366f03f71",
      "group_code": null,
      "tracked_at": "2016-06-27T13:38:55.455Z",
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

This endpoint authenticate by patron authenticate, and retrieves all transactions for specific
patron and for specific establishment

### HTTP Request

`GET http://example.com/api/patrons/establishments`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
establishment_id | Y | establishment_id that transactions belongs to
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20
