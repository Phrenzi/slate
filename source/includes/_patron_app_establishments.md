# PatronApp / Establishments

## get all establishments

```shell
curl "https://phrenzi.com/api/patron_app/establishments" \
  -H "Content-Type: application/json" \
```

> The above command returns JSON structured like this:

```json
{
  "establishments": [
    {
      "id": "c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea",
      "name": "Establishment1",
      "phone": "612345671",
      "cash_back": "3.5",
      "desc": "This is an example description",
      "logo_url": "http://abc.com/uploads/establishment/logo/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/thumb_image.jpeg",
      "banner_url": "http://abc.com/uploads/establishment/banner/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/thumb_image.jpeg",
      "active_booster_count": 3,
      "credit_balance": "20000.0"
    },
    {
      "id": "0c9d3e1c-9499-472c-8f87-9acd0f8866d2",
      "name": "Establishment2",
      "phone": "612345672",
      "cash_back": "3.5",
      "desc": "This is an example description",
      "logo_url": "http://abc.com/uploads/establishment/logo/0c9d3e1c-9499-472c-8f87-9acd0f8866d2/thumb_image.jpeg",
      "banner_url": "http://abc.com/uploads/establishment/banner/0c9d3e1c-9499-472c-8f87-9acd0f8866d2/thumb_image.jpeg",
      "active_booster_count": 0,
      "credit_balance": "200.0"
    }
  ]
}
```

This endpoint retrieves all establishments

### HTTP Request

`GET http://example.com/api/patron_app/establishments`

<aside class="warning">We will add pagination parameter later, but for this phase, we just skip it.</aside>


## get establishment

```shell
curl "https://phrenzi.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea" \
  -H "Content-Type: application/json" \
```

> The above command returns JSON structured like this:

```json
{
  "establishment": {
    "id": "610ce5ee-8ce2-4ad2-9296-3e2bd6ec539a",
    "name": "Establishment1",
    "phone": "612345671",
    "cash_back": "3.5",
    "desc": "This is an example description",
    "logo_url": "http://abc.com/uploads/establishment/logo/e1c3c3b9e1bb587672ed14663c233d2a.jpeg",
    "banner_url": "http://abc.com/uploads/establishment/banner/cf2731b3f037e081fee8230378290b62.jpeg",
    "active_booster_count": 3,
    "credit_balance": "20000.0",
    "address": {
      "id": "54f27047-8a98-4304-b7bc-43b2f855a582",
      "street1": "MyString",
      "street2": "MyString",
      "city": "MyString",
      "country": "MyString"
    },
    "business_hours": [
      {
        "wday": 0,
        "open_time": 39600,
        "close_time": 86400,
        "closed": false
      },
      {
        "wday": 1,
        "open_time": 39600,
        "close_time": 86400,
        "closed": false
      },
      {
        "wday": 2,
        "open_time": 39600,
        "close_time": 86400,
        "closed": false
      },
      {
        "wday": 3,
        "open_time": 39600,
        "close_time": 86400,
        "closed": false
      },
      {
        "wday": 4,
        "open_time": 39600,
        "close_time": 86400,
        "closed": false
      },
      {
        "wday": 5,
        "open_time": 39600,
        "close_time": 86400,
        "closed": false
      },
      {
        "wday": 6,
        "open_time": 39600,
        "close_time": 86400,
        "closed": false
      }
    ]
  },
  "current_challenge": {
    "start_date": "2016-12-06T16:00:00.000Z",
    "end_date": "2016-12-06T16:00:00.000Z",
    "winner_percentage": "25.0",
    "prize_percentage": "5.0",
    "total_sales": "10000.0",
    "ranking": [
      {
        "id": "f9128d9c-a60c-471d-8e22-761bc0a0a785",
        "name": "Patron2",
        "join_time": "2016-12-07T12:30:01.496Z",
        "point_balance": "20.0",
        "ranking": 0,
        "prize": "500"
      },
      {
        "id": "8d7c84fd-c6d1-4c02-b7b6-e5a3d6eebacd",
        "name": "Patron1",
        "join_time": "2016-12-07T12:30:01.469Z",
        "point_balance": "10.0",
        "ranking": 1,
        "prize": "0.0"
      }
    ]
  }
}
```

This endpoint retrieves establishment detail

### HTTP Request

`GET http://example.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea`
