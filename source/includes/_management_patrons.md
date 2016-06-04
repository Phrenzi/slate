# Management / Patrons

## Get all patrons

```shell
curl "https://phrenzi.com/api/v1/management/patrons"
  -H "Authorization: your_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "ASDSDS",
    "name": "Simon Iong",
    "balance": 123.32
  },
  {
    "id": "ASDDD",
    "name": "Max Max",
    "balance": 124.44
  }
]
```

This endpoint require manager token, and retrieves all patrons.

### HTTP Request

`POST http://phrenzi.com/api/v1/management/patrons`
