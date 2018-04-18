# PatronApp / Point Transactions

## get all point transactions by establishment_id

```shell
curl "https://phrenzi.com/api/patron_app/point_transactions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -d '{
    "establishment_id": "d51dd6c5-ad0e-445f-b3c5-06ab8ec8624b"
    }'
```

> The above command returns JSON structured like this:

```json
{
  "transactions": [
    {
      "id": "86649ff8-abb4-4e4f-9a64-16607ccac2f4",
      "patron_id": "437d5272-e694-41cb-8c4f-12c0f37f3588",
      "establishment_id": "d51dd6c5-ad0e-445f-b3c5-06ab8ec8624b",
      "booster_id": null,
      "challenge_id": "4972f2df-d378-4f87-b9c9-ac45ab12d0ac",
      "point": "9.99",
      "point_balance": "19.99",
      "trans_code": "394548216b",
      "action": "Purchase Points",
      "correction": false,
      "tracked_at": "2017-05-12T03:02:32Z"
    },
    {
      "id": "9bea46d0-d077-4d0b-beaa-5b11151601d4",
      "patron_id": "437d5272-e694-41cb-8c4f-12c0f37f3588",
      "establishment_id": "d51dd6c5-ad0e-445f-b3c5-06ab8ec8624b",
      "booster_id": null,
      "challenge_id": "4972f2df-d378-4f87-b9c9-ac45ab12d0ac",
      "point": "9.99",
      "point_balance": "19.99",
      "trans_code": "a3ace99530",
      "action": "Purchase Points",
      "correction": false,
      "tracked_at": "2017-05-12T03:02:31Z"
    }
  ]
}
```

This endpoint authenticate by `Patron Token`, and retrieves all transactions for specific patron and for specific establishment

### HTTP Request

`GET http://example.com/api/patron_app/point_transactions`

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
establishment_id | Y | establishment_id that transactions belongs to
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20
