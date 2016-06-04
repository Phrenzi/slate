# Establishments

## get all establishments

```shell
curl "https://phrenzi.com/api/v1/establishments"
  -H "Authorization: your_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint required user authenticate, and retrieves all establishments

### HTTP Request

`GET http://example.com/api/v1/establishments`

<aside class="warning">We will add pagination parameter later, but for this phase, we just skip it.</aside>
