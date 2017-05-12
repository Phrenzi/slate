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
    "establishment_id": "d51dd6c5-ad0e-445f-b3c5-06ab8ec8624b"
    }'
```

> The above command returns JSON structured like this:

```json
{
  "transactions": [
    {
      "id": "3e2d1786-3379-4311-93c4-86ac85cb6fc3",
      "patron_id": "cd4820df-0572-4e06-a60b-2411fd450272",
      "establishment_id": "d51dd6c5-ad0e-445f-b3c5-06ab8ec8624b",
      "challenge_id": null,
      "trans_type": "sales",
      "sales_amount": "100.0",
      "applied_credit": "0.0",
      "sales_credit": "3.5",
      "credit_subtotal": "3.5",
      "remaining_credit": "0.0",
      "cash_back": "3.5",
      "trans_code": "0cd28c0d26",
      "group_code": null,
      "tracked_at": "2017-03-29T19:09:43.791+08:00",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    },
    {
      "id": "c294a412-b391-44c5-8cc7-25a4f4b1a7b5",
      "patron_id": "cd4820df-0572-4e06-a60b-2411fd450272",
      "establishment_id": "d51dd6c5-ad0e-445f-b3c5-06ab8ec8624b",
      "challenge_id": null,
      "trans_type": "sales",
      "sales_amount": "100.0",
      "applied_credit": "0.0",
      "sales_credit": "3.5",
      "credit_subtotal": "3.5",
      "remaining_credit": "0.0",
      "cash_back": "3.5",
      "trans_code": "8c36accb11",
      "group_code": null,
      "tracked_at": "2017-03-29T19:09:43.791+08:00",
      "del_transaction_id": null,
      "deleted_at": null,
      "deleted": false
    }
  ]
}
```

This endpoint authenticate by patron authenticate, and retrieves all transactions for specific
patron and for specific establishment

### HTTP Request

`GET http://example.com/api/patron_app/establishments`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
establishment_id | Y | establishment_id that transactions belongs to
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20
