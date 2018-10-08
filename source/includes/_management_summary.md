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
