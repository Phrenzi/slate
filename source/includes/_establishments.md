# Establishments

## get all establishments

```shell
curl "https://phrenzi.com/api/establishments" \
  -H "Content-Type: application/json" \
  -H "Authorization: app_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "WE7EASD",
    "name": "Awesome Bar",
    "phone": "92342333",
    "desc": "this is a sample description",
    "cash_back": 3.5,
    "address": {
      "street1": "street 1 example",
      "street2": "street 2 example",
      "city": "Hong Kong",
      "country": "Hong Kong"
    },
    "business_hours": [
      { 
        "wday": 0,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 1,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 2,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 3,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 4,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 5,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 6,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      }]
  },
  {
    "id": "WE7EASD",
    "name": "Awesome Bar 2",
    "phone": "92342333",
    "desc": "this is a sample description",
    "cash_back": 3.5,
    "address": {
      "street1": "street 1 example",
      "street2": "street 2 example",
      "city": "Hong Kong",
      "country": "Hong Kong"
    },
    "business_hours": [
      { 
        "wday": 0,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 1,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 2,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 3,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 4,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 5,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      },
      { 
        "wday": 6,
        "open_time": 1234123123,
        "close_time": 1244444433,
        "closed": false
      }]
  }
]
```

This endpoint authenticate by `app_token`, and retrieves all establishments

### HTTP Request

`GET http://example.com/api/establishments`

<aside class="warning">We will add pagination parameter later, but for this phase, we just skip it.</aside>
