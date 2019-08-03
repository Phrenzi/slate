# PatronApp / Establishments

## get all establishments

```shell
curl "https://phrenzi.com/api/patron_app/establishments" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
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
      "user_active_booster_count": 3,
      "credit_balance": "20000.0",
      "favorite": true,
      "locations": [
        {
          "id": "07b732fd-225f-445a-99ac-23828daaeab1",
          "name": "location",
          "desc": "ocation desc",
          "lat": "1.2323",
          "long": "1.23333"
        }
      ]
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
      "user_active_booster_count": 0,
      "credit_balance": "200.0",
      "favorite": true,
      "locations": [
        {
          "id": "07b732fd-225f-445a-99ac-23828daaeab1",
          "name": "another location",
          "desc": "location desc",
          "lat": "1.2323",
          "long": "1.23333"
        }
      ]
    }
  ]
}
```

This endpoint use `Patron Token`, and retrieves all establishments.

### HTTP Request

`GET http://example.com/api/patron_app/establishments`

<aside class="warning">We will add pagination parameter later, but for this phase, we just skip it.</aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
type | N | 'favorite' or nothing

## get establishment

```shell
curl "https://phrenzi.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
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
    "user_active_booster_count": 3,
    "credit_balance": "20000.0",
    "favorite": false,
    "locations": [
      {
        "id": "07b732fd-225f-445a-99ac-23828daaeab1",
        "name": "another location",
        "desc": "location desc",
        "lat": "1.2323",
        "long": "1.23333"
      }
    ],
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
    "start_date": "2016-12-06T16:00:00Z",
    "end_date": "2016-12-06T16:00:00Z",
    "prize_percentage": "25.0",
    "max_payout_rank": 5,
    "total_sales": "10000.0",
    "ranking": [
      {
        "id": "f9128d9c-a60c-471d-8e22-761bc0a0a785",
        "first_name": "Patron2",
        "last_name": "Last2",
        "join_time": "2016-12-07T12:30:01Z",
        "profile_url": "http://abc.com/uploads/patron/profile/cf2731b3f037e081fee8230378290b62.jpeg",
        "point_balance": "20.0",
        "ranking": 0,
        "prize": "500"
      },
      {
        "id": "8d7c84fd-c6d1-4c02-b7b6-e5a3d6eebacd",
        "first_name": "Patron1",
        "last_name": "Last1",
        "join_time": "2016-12-07T12:30:01Z",
        "profile_url": "http://abc.com/uploads/patron/profile/cf2731b3f037e081fee8230378290b62.jpeg",
        "point_balance": "10.0",
        "ranking": 1,
        "prize": "0.0"
      }
    ]
  }
}
```

This endpoint use `Patron Token` and retrieves establishment detail

### HTTP Request

`GET http://example.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea`


## favorite establishment

```shell
curl
"https://phrenzi.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/favorite" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X POST
```

> if okay, The above command returns status code 200 and empty json;

This endpoint use `Patron Token` and retrieves establishment detail

### HTTP Request

`POST http://example.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/favorite`

## unfavorite establishment

```shell
curl
"https://phrenzi.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/favorite" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X DELETE
```

> if okay, The above command returns status code 200 and empty json;


This endpoint use `Patron Token` and retrieves establishment detail

### HTTP Request

`DELETE http://example.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/favorite`
