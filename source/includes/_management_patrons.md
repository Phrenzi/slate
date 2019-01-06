# Management / Patrons

## Get all patrons

```shell
curl "https://phrenzi.com/api/management/patrons" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> The above command returns array of `Patron` object like this:

```json
{
  "patrons": [
    {
      "id": "8d3d7ecd-585d-4f2f-ad21-1b457e062681",
      "name": "F1 L1",
      "first_name": "F1",
      "last_name": "L1",
      "email": "patron1@gmail.com",
      "credit_balance": "100.23",
      "trans_code": "52553b",
      "profile": "https://phrenzi.com/uploads/cache/a8a70be864925f7bddc0bcf93fa89986.jpeg"
    },
    {
      "id": "fcbdd18f-e5ea-4368-8cf4-2e688e604a40",
      "name": "F2 L2",
      "first_name": "F2",
      "last_name": "L2",
      "email": "patron2@gmail.com",
      "credit_balance": "0.0",
      "trans_code": "25e8ac",
      "profile": "https://phrenzi.com/uploads/cache/a8a70be864925f7bddc0bcf93fa89986.jpeg"
    },
    {
      "id": "c3335da8-a771-4974-8756-007be2530490",
      "name": "Frist001 Last001",
      "first_name": "Frist001",
      "last_name": "Last001",
      "email": "patron1@gmail.com",
      "credit_balance": "100.23",
      "trans_code": "af019e",
      "profile": "/uploads/cache/2eb90e2645050f0b6bbcff902c5c3661.jpeg",
      "challenge": {
        "point_balance": 10,
        "prize": "0.0",
        "ranking": 1
      }
    },
    {
      "id": "0ea9dedb-4c6e-422d-92fd-ccb8d8db168c",
      "name": "Frist002 Last002",
      "first_name": "Frist002",
      "last_name": "Last002",
      "email": "patron2@gmail.com",
      "credit_balance": "0.0",
      "trans_code": "ad215c",
      "profile": "/uploads/cache/b12a9a4a1de551aee65a33dba8509692.jpeg",
      "challenge": {
        "point_balance": 20,
        "prize": "500.0",
        "ranking": 0
      }
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and retrieves all patrons.

Noted that credit_balance returned from patron object is for manager's establishment,
the `credit_balance` return from different manager authenticated should be differernt.

### HTTP Request

`GET http://phrenzi.com/api/management/patrons`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
filter | N | filter options, for now, only accept 'favorite'
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20

## Get patron

```shell
curl "https://phrenzi.com/api/management/patrons/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
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

This endpoint authenticated by `Manger Token`, and retrieves patron object.

Noted that credit_balance returned from patron object is for manager's establishment,
the `credit_balance` return from different manager authenticated should be differernt.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

### HTTP Request

`GET http://phrenzi.com/api/management/patrons/ddbd0c3c-404d-4ce1-9042-9baecb4ef585`
