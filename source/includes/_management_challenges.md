# Management / Challenges

## Get all challenges

```shell
curl "https://phrenzi.com/api/management/challenges" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -d '{
    "start": "2018-03-01",
    "end": "2018-03-28"
    }'

```

> The above command returns array of `Challenges` objects:

```json
{
  "challenges": [
    {
      "id": "651b9916-53e4-4db9-8ccb-8d4108fbfed8",
      "identity": "651b9916",
      "start_date": "2018-04-01",
      "end_date": "2018-04-02",
      "status": "scheduled"
    },
    {
      "id": "107acf53-d591-4a9b-aea4-580936d542ce",
      "identity": "107acf53",
      "start_date": "2018-04-03",
      "end_date": "2018-04-04",
      "status": "scheduled"
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and Staff-ID Request Haeder, staff should be manager staff, and retrieves all challenges.

### HTTP Request

`GET http://phrenzi.com/api/management/challenges`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
start | Y | start range of query, format: 'YYYY-MM-DD'
end | Y | end range of query, format: 'YYYY-MM-DD'
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20
