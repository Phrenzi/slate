# Management / Report

## Get daily summaries

```shell
curl "https://phrenzi.com/api/management/daily_summaries" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -d '{
    "start_date": "2018-10-08",
    "end_date": "2018-10-09"
    }'
```

> The above command returns array of `Booster` objects:

```json
{
  "summaries": [
    {
      "id": "c05714a2-1929-4183-be62-8051ed869da5",
      "date": "2018-10-09",
      "file_url": "/uploads/cache/495efe5be347bdc0c99c303809196731.pdf"
    },
    {
      "id": "9931bb61-de01-401c-8eff-53ec3cafaed9",
      "date": "2018-10-08",
      "file_url": "/uploads/cache/966551a5526e9bab012e960cedf37786.pdf"
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and return daily summaries report

### HTTP Request

`GET http://phrenzi.com/api/management/daily_summaries`

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
start_date | Y | start range of query, format: 'YYYY-MM-DD'
end_date | Y | end range of query, format: 'YYYY-MM-DD'
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 50



## Get monthly summaries / monthly invoices & receipts

```shell
curl "https://phrenzi.com/api/management/monthly_summaries" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -d '{
    "start_date": "2018-09-01",
    "end_date": "2018-11-01"
    }'
```

> The above command returns array of `Booster` objects:

```json
{
  "summaries": [
    {
      "id": "5522331f-eddd-4bf6-a832-69c1b076eb4d",
      "date": "2018-11-01",
      "invoice_url": "/uploads/cache/2b20eeef5cf2dbf25eac615322cc7eb4.pdf"
    },
    {
      "id": "d8483110-56f7-4a43-bcae-b5c37cf511f2",
      "date": "2018-10-01",
      "invoice_url": "/uploads/cache/9c1138bc4c12f2ac3e796d36c9378c5d.pdf",
      "receipt_url": "/uploads/cache/420da87ea611eac320c37b78c2382926.pdf"
    },
    {
      "id": "10de5f01-84ee-437b-88bf-694d93ffefc2",
      "date": "2018-09-01",
      "invoice_url": "/uploads/cache/18374e5fbbd158e4baed64d0930fd9e2.pdf",
      "receipt_url": "/uploads/cache/741c038e73871819e27b8ec0b8e2a7e5.pdf"
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and return monthly summaries report

### HTTP Request

`GET http://phrenzi.com/api/management/monthly_summaries`

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
start_date | Y | start range of query, format: 'YYYY-MM-DD'
end_date | Y | end range of query, format: 'YYYY-MM-DD'
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 50
