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

> The above command returns array of `Challenge` objects:

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

This endpoint authenticated by `Manager Token`, and Staff-ID Request Header, staff should be manager staff, and retrieves all challenges.

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

## Create Challenge

```shell
curl "https://phrenzi.com/api/management/challenges" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X POST \
  -d '{
    "start_date": "2018-03-01",
    "end_date": "2018-03-07",
    "max_payout_rank": 10,
    "prize_percentage": 15
    }'
```

> The above command returns `Challenge` objects:

```json
{
  "challenge": {
    "id": "a635683c-87d3-4531-a5b5-f58d44d053b8",
    "identity": "a635683c",
    "start_date": "2018-03-31",
    "end_date": "2018-04-01",
    "status": "scheduled"
  }
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and create Challenge

### HTTP Request

`POST http://phrenzi.com/api/management/challenges`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
start_date | Y | start date of challenge
end_date | Y | end date of challenge
max_payout_rank | N | the maximum payout ranking, if not present, system setting will be used
prize_percentage | N | the prize percentage, if not present, system setting will be used

## Update Challenge

```shell
curl "https://phrenzi.com/api/management/challenges/a635683c-87d3-4531-a5b5-f58d44d053b8" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "start_date": "2018-03-01",
    "end_date": "2018-03-07",
    "max_payout_rank": 10,
    "prize_percentage": 15
    }'
```

> The above command returns `Challenge` objects:

```json
{
  "challenge": {
    "id": "a635683c-87d3-4531-a5b5-f58d44d053b8",
    "identity": "a635683c",
    "start_date": "2018-03-31",
    "end_date": "2018-04-01",
    "status": "scheduled"
  }
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and update Challenge

### HTTP Request

`PATCH http://phrenzi.com/api/management/challenges/:challenge_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
start_date | Y | start date of challenge
end_date | Y | end date of challenge
max_payout_rank | N | the maximum payout ranking, if not present, system setting will be used
prize_percentage | N | the prize percentage, if not present, system setting will be used

## Delete Challenge

```shell
curl "https://phrenzi.com/api/management/challenges/a635683c-87d3-4531-a5b5-f58d44d053b8" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X DELETE
```

> If success, return 200 status code with empty response.

> If failed, return 406 status code with error message:

```
{
  "errors": [
    "can not delete non-scheduled challenges"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and update Challenge

### HTTP Request

`DELETE http://phrenzi.com/api/management/challenges/:challenge_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

## Stop Challenge

```shell
curl "https://phrenzi.com/api/management/challenges/a635683c-87d3-4531-a5b5-f58d44d053b8/stop" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH
```

> If success, return 200 status code with empty response.

> If failed, return 406 status code with error message:

```
{
  "errors": [
    "can not stop challenge that is not active"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and stop Challenge

### HTTP Request

`PATCH http://phrenzi.com/api/management/challenges/:challenge_id/stop`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>
