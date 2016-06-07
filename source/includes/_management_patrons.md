# Management / Patrons

## Get all patrons

```shell
curl "https://phrenzi.com/api/management/patrons"
  -H "Authorization: manager_token"
```

> The above command returns array of `Basic Patron` object like this:

```json
[
  {
    "id": "ASDSDS",
    "name": "Simon Iong",
    "credit_balance": 123.32
  },
  {
    "id": "ASDDD",
    "name": "Max Max",
    "credit_balance": 124.44
  }
]
```

This endpoint require `manager_token`, and retrieves all patrons.

### HTTP Request

`GET http://phrenzi.com/api/management/patrons`
