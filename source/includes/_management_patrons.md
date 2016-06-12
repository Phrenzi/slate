# Management / Patrons

## Get all patrons

```shell
curl "https://phrenzi.com/api/management/patrons" \
  -H "Content-Type: application/json" \
```

> The above command returns array of `Patron` object like this:

```json
{
  "data": [
    {
      "id": "8654d532-bd5a-4b0f-acf4-08dbbbd0a01f",
      "type": "patrons",
      "attributes": {
        "email": "abc1@gmail.com",
        "credit-balance": "0.0",
        "trans-code": "773c1a"
      }
    },
    {
      "id": "25084757-de90-4ed7-88be-e5701f2ff248",
      "type": "patrons",
      "attributes": {
        "email": "abc2@gmail.com",
        "credit-balance": "0.0",
        "trans-code": "8c346c"
      }
    }
  ]
}
```

This endpoint require `manager authenticate`, and retrieves all patrons.

### HTTP Request

`GET http://phrenzi.com/api/management/patrons`
