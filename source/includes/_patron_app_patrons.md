# PatronApp / Patrons

## Get all patrons

```shell
curl "https://phrenzi.com/api/patron_app/patrons" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
```

> The above command returns array of `Patron` object like this:

```json
{
  "patrons": [
    {
      "id": "abfd977f-9f3c-41ef-b920-730ab0adabdc",
      "first_name": "F1",
      "last_name": "David",
      "profile": "https://phrenzi.com/uploads/cache/a8a70be864925f7bddc0bcf93fa89986.jpeg",
      "join_date": "2017-06-29T16:34:46Z",
      "favorite_establishments": [
        {
          "id": "551136c7-11dd-449d-abd1-047f49c0229e",
          "name": "Cafe Roma",
          "logo_url": "/uploads/cache/6f6c813b759d1356b4df3d708cc67b43.jpeg",
          "address_city": "MyString"
        },
        {
          "id": "d0d5cbe6-9319-4f5e-accc-54ad85826054",
          "name": "Awesome Bar",
          "logo_url": "/uploads/cache/3f07b695b94bfbfe1a3e9f1086d13db5.jpeg",
          "address_city": "MyString"
        }
      ],
      "friend_status": "friend"
    },
    {
      "id": "8fc7cb28-a38c-4830-8488-4a8bd68f552a",
      "first_name": "F2",
      "last_name": "Kerry",
      "profile": "https://phrenzi.com/uploads/cache/12370be864925f7bddc0bcf93fa89123.jpeg",
      "join_date": "2017-06-29T16:34:46Z",
      "favorite_establishments": [],
      "friend_status": "normal"
    }
  ]
}

```

This endpoint require `Patron Token` authentication, and retrieves all patrons.

### HTTP Request

`GET http://phrenzi.com/api/patron_app/patrons`

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
type | N | type could be: 'normal', 'pending', 'friend', used to filter patron list result
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20
