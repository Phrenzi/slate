# Management / Patrons

## Get all patrons

```shell
curl "https://phrenzi.com/api/management/patrons" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> The above command returns array of `Patron` object like this:

```json
{
  "patrons": [
    {
      "id": "b6ce5873-49b9-4c01-b8a0-7102a88ed6be",
      "name": "Frist001 Last001",
      "first_name": "Frist001",
      "last_name": "Last001",
      "email": null,
      "phone_number": "66762659",
      "country_code": "853",
      "credit_balance": "100.23",
      "trans_code": "b8b458",
      "profile": "/uploads/cache/2b13270129d91b98c1e8ab26b0d08af4.jpeg"
    },
    {
      "id": "c6ce5873-49b9-4c01-b8a0-7102a88ed6be",
      "name": "Frist001 Last001",
      "first_name": "Frist001",
      "last_name": "Last001",
      "email": "patron1@gmail.com",
      "phone_number": null,
      "country_code": null,
      "credit_balance": "100.23",
      "trans_code": "b8b458",
      "profile": "/uploads/cache/2b13270129d91b98c1e8ab26b0d08af4.jpeg"
    },
    {
      "id": "a6ce5873-49b9-4c01-b8a0-7102a88ed6be",
      "name": "Frist001 Last001",
      "first_name": "Frist001",
      "last_name": "Last001",
      "email": "patron2@gmail.com",
      "phone_number": null,
      "country_code": null,
      "credit_balance": "100.23",
      "trans_code": "b8b458",
      "profile": "/uploads/cache/2b13270129d91b98c1e8ab26b0d08af4.jpeg",
      "challenge": {
        "point_balance": 20,
        "prize": "500.0",
        "ranking": 0
      }
    },
    {
      "id": "c0e4e6af-1591-40aa-bd44-9ba75ea3ba86",
      "name": "Frist002 Last002",
      "first_name": "Frist002",
      "last_name": "Last002",
      "email": "patron3@gmail.com",
      "phone_number": null,
      "country_code": null,
      "credit_balance": "0.0",
      "trans_code": "39657e",
      "profile": "/uploads/cache/0be78d68c1a33a67d2115c5ee8ff902a.jpeg",
      "challenge": {
        "point_balance": 10,
        "prize": "0.0",
        "ranking": 1
      }
    }
  ]
}
```

This endpoint authenticated by `Access Token`, and retrieves all patrons.

Noted that credit_balance returned from patron object is for manager's establishment,
the `credit_balance` return from different manager authenticated should be differernt.

### HTTP Request

`GET http://phrenzi.com/api/management/patrons`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">due to technical reason, This API DO NOT SUPPORT Link Response Header pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
keyword | N | keyword options, for now, buzz search for patron name or phone number
filter | N | filter options, for now, only accept 'favorite'
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20

## Get patron

```shell
curl "https://phrenzi.com/api/management/patrons/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer access_token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> The above command return `Patron` object like this:

```json
{
  "patron": {
    "id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
    "first_name": "F1",
    "last_name": "L1",
    "email": "patron1@gmail.com",
    "phone_number": null,
    "country_code": null,
    "credit_balance": "100.23",
    "trans_code": "519665",
    "profile": "https://phrenzi.com/uploads/cache/a8a70be864925f7bddc0bcf93fa89986.jpeg",
    "stats": {
      "challenge_played": 1,
      "challenge_won": 0,
      "prize_earned": "23.23",
      "point_earned": "200.0",
      "booster_earned": 13,
      "credit_earned_from_correction": "100.0",
      "credit_loss_from_correction": "100.0",
      "credit_earned_from_cash": "100.0",
      "credit_spent": "100.0",
      "credit_earned_from_deletion": "100.0",
      "credit_loss_from_deletion": "100.0",
      "credit_earned_from_prize": "100.0"
    }
  }
}
```

This endpoint authenticated by `Access Token`, and retrieves patron object.

Noted that credit_balance returned from patron object is for manager's establishment,
the `credit_balance` return from different manager authenticated should be differernt.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

### HTTP Request

`GET http://phrenzi.com/api/management/patrons/ddbd0c3c-404d-4ce1-9042-9baecb4ef585`
