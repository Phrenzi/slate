# Management / Tasks

## Get all active task boosters

```shell
curl "https://phrenzi.com/api/management/tasks" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -d '{
    "patron_id": "8d3d7ecd-585d-4f2f-ad21-1b457e062681"
    }'

```

> The above command returns array of `Task Booster` object like this:

```json
{
  "tasks": [
    {
      "id": "25fe526b-04da-407b-84a3-a497c26fb628",
      "booster_type": "task",
      "status": "actived",
      "start_time": "2017-10-10T04:53:20Z",
      "point": "100.0",
      "finished_by": "end_time",
      "task_desc": "Sing a Song",
      "end_time": "2017-10-10T05:03:20Z",
      "patron": {
        "redeemed": true,
        "redeemed_at": "2017-10-10T05:00:00Z"
      }
    },
    {
      "id": "7bd71f62-7f00-40ab-8104-ff9afd8219f3",
      "booster_type": "task",
      "status": "actived",
      "start_time": "2017-10-10T04:55:00Z",
      "point": "100.0",
      "finished_by": "end_time",
      "task_desc": "Sing a love Song",
      "end_time": "2017-10-10T05:03:20Z",
      "patron": {
        "redeemed": false
      }
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and retrieves all active task boosters along with redeemed information with patron_id selected

### HTTP Request

`GET http://phrenzi.com/api/management/tasks`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
patron_id | Y | the patron's id for task booster's redeem information
page | N | the page results of all transactions
per_page | N | the number of transaction record return per page by api, default to be 20

## Redeem Task

```shell
curl "https://phrenzi.com/api/management/tasks/ddbd0c3c-404d-4ce1-9042-9baecb4ef585/redeem" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "patron_id": "8d3d7ecd-585d-4f2f-ad21-1b457e062681"
    }'

```

> The above command return status code 200 and json response like this:

```json
{
  "messages": [
    "redeem task successs"
  ]
}
```

> If patron is already redeemed, return status code 406 and json response:

```json
{
  "errors": [
    "Already redeemed"
  ]
}
```

> If patron_id is not provied, return status code 422 and json response:

```json
{
  "errors": [
    "patron_id is required"
  ]
}
```

> If required task booster is not actived or do not have active challenge right now, return status code 406 and json response:

```json
{
  "errors": [
    "There is no active Challenge or Booster today"
  ]
}
```

This endpoint authenticated by `Manger Token`, and redeem task booster for patron provieded.

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>
### HTTP Request

`PATCH http://phrenzi.com/api/management/tasks/:task_id/redeem`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
patron_id | Y | the patron's id for task booster's redeem information
