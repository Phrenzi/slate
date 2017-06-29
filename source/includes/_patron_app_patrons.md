# PatronApp / Patrons

## Get all patrons

```shell
curl "https://phrenzi.com/api/patron_app/patrons" \
  -H "Content-Type: application/json"
```

> The above command returns array of `Patron` object like this:

```json
{
  "patrons": [
    {
      "id": "abfd977f-9f3c-41ef-b920-730ab0adabdc",
      "name": "David",
      "profile": "https://phrenzi.com/uploads/cache/a8a70be864925f7bddc0bcf93fa89986.jpeg",
      "created_at": "2017-06-29T16:34:46Z"
    },
    {
      "id": "8fc7cb28-a38c-4830-8488-4a8bd68f552a",
      "name": "Kerry",
      "profile": "https://phrenzi.com/uploads/cache/12370be864925f7bddc0bcf93fa89123.jpeg",
      "created_at": "2017-06-29T16:34:46Z"
    }
  ]
}

```

This endpoint require patron authentication, and retrieves all patrons.

### HTTP Request

`GET http://phrenzi.com/api/patron_app/patrons`

<aside class="info">This API support pagination. please refer to <a
href="#link-header-result-pagination">Link Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20