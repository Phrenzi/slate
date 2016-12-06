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
    "id": "c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea",
    "name": "Establishment1",
    "phone": "612345671",
    "cash_back": "3.5",
    "desc": "This is an example description",
    "logo_url": "http://abc.com/uploads/establishment/logo/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/thumb_image.jpeg",
    "banner_url": "http://abc.com/uploads/establishment/banner/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/thumb_image.jpeg",
    "business_hours": [
      {
        "wday": 0,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "wday": 1,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "wday": 2,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "wday": 3,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "wday": 4,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "wday": 5,
        "open_time": 39600,
        "close_time": 86400
      },
      {
        "wday": 6,
        "open_time": 39600,
        "close_time": 86400
      }
    ],
    "address": {
      "id": "0485af50-a837-4545-aeac-db9877637f46",
      "street1": "MaWan",
      "street2": "",
      "city": "Hong Kong",
      "country": "HK"
    }
  },
  "current_challenge": {
    "winner_percentage": "5.0",
    "prize_percentage": "25.0",
    "total_sales": "12345600.0",
    "start_date": "2016-12-12 00:00:00",
    "end_date": "2016-12-13 00:00:00"
  },
  "current_boosters": [
    { "id": "0485af50-a837-4545-aeac-db9877637f56",
      "status": "scheduled",
      "booster_type": "check_in",
      "start_time": "2016-12-12 00:00:00",
      "end_time": "2016-12-12 01:00:00"
    },
    { "id": "0485af50-a837-4545-aeac-dc9877637f56",
      "status": "finished",
      "booster_type": "check_in",
      "start_time": "2016-12-12 00:00:00",
      "end_time": "2016-12-12 01:00:00"
    },
    { "id": "0485af50-a837-4545-aeac-da9877637f56",
      "status": "actived",
      "booster_type": "target_amount",
      "start_time": "2016-12-12 00:00:00",
      "end_time": "2016-12-12 01:00:00"
    },
    { "id": "0485af50-a837-4545-aeac-de9877637f56",
      "status": "scheduled",
      "booster_type": "target_amount",
      "start_time": "2016-12-12 00:00:00",
      "end_time": "2016-12-12 01:00:00"
    },
    { "id": "0485af50-a837-4545-aeac-d59877637f56",
      "status": "scheduled",
      "booster_type": "invitation",
      "start_time": "2016-12-12 00:00:00",
      "end_time": "2016-12-12 01:00:00"
    }
  ]
}
```

This endpoint retrieves establishment detail

### HTTP Request

`GET http://example.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea`
