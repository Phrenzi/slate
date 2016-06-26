# Establishments

## get all establishments

```shell
curl "https://phrenzi.com/api/establishments" \
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
    {
      "id": "0c9d3e1c-9499-472c-8f87-9acd0f8866d2",
      "name": "Establishment2",
      "phone": "612345672",
      "cash_back": "3.5",
      "desc": "This is an example description",
      "logo_url": "http://abc.com/uploads/establishment/logo/0c9d3e1c-9499-472c-8f87-9acd0f8866d2/thumb_image.jpeg",
      "banner_url": "http://abc.com/uploads/establishment/banner/0c9d3e1c-9499-472c-8f87-9acd0f8866d2/thumb_image.jpeg",
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
        "id": "f6eefa86-42d0-4786-bd3c-d4c9ecc4abb1",
        "street1": "MaWan",
        "street2": "",
        "city": "Hong Kong",
        "country": "HK"
      }
    }
  ]
}
```

This endpoint retrieves all establishments

### HTTP Request

`GET http://example.com/api/establishments`

<aside class="warning">We will add pagination parameter later, but for this phase, we just skip it.</aside>
