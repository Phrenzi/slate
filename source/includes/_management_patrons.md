# Management / Patrons

## Get all patrons

```shell
curl "https://phrenzi.com/api/management/patrons" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> The above command returns array of `Patron` object like this:

```json
{
  "patrons": [
    {
      "id": "8d3d7ecd-585d-4f2f-ad21-1b457e062681",
      "first_name": "F1",
      "last_name": "L1",
      "email": "patron1@gmail.com",
      "credit_balance": "100.23",
      "trans_code": "52553b",
      "profile": "https://phrenzi.com/uploads/cache/a8a70be864925f7bddc0bcf93fa89986.jpeg"
    },
    {
      "id": "fcbdd18f-e5ea-4368-8cf4-2e688e604a40",
      "first_name": "F2",
      "last_name": "L2",
      "email": "patron2@gmail.com",
      "credit_balance": "0.0",
      "trans_code": "25e8ac",
      "profile": "https://phrenzi.com/uploads/cache/a8a70be864925f7bddc0bcf93fa89986.jpeg"
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and retrieves all patrons.

Noted that credit_balance returned from patron object is for manager's establishment,
the `credit_balance` return from different manager authenticated should be differernt.

### HTTP Request

`GET http://phrenzi.com/api/management/patrons`

<aside class="info">This API support pagination. please refer to <a
href="#link-header-result-pagination">Link Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20

## Get patron

```shell
curl "https://phrenzi.com/api/management/patrons/ddbd0c3c-404d-4ce1-9042-9baecb4ef585" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> The above command return `Patron` object like this:

```json
{
  "patron": {
    "id": "ddbd0c3c-404d-4ce1-9042-9baecb4ef585",
    "first_name": "F1",
    "last_name": "L1",
    "email": "patron1@gmail.com",
    "credit_balance": "100.23",
    "trans_code": "519665",
    "profile": "https://phrenzi.com/uploads/cache/a8a70be864925f7bddc0bcf93fa89986.jpeg"
  }
}
```

This endpoint authenticated by `Manger Token`, and retrieves patron object.

Noted that credit_balance returned from patron object is for manager's establishment,
the `credit_balance` return from different manager authenticated should be differernt.

### HTTP Request

`GET http://phrenzi.com/api/management/patrons/ddbd0c3c-404d-4ce1-9042-9baecb4ef585`
