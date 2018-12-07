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

## Get Challenge

```shell
curl "https://phrenzi.com/api/management/challenges/7a6cd829-1328-44dc-abdd-eda6e2d2f64a" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

> The above command returns array of `Challenge` objects:

```json
{
  "challenge": {
    "id": "7a6cd829-1328-44dc-abdd-eda6e2d2f64a",
    "identity": "7a6cd829",
    "start_date": "2018-03-30",
    "end_date": "2018-03-31",
    "status": "actived",
    "total_sales": "10000.0",
    "max_payout_rank": 5,
    "prize_percentage": "10.0",
    "ranking": [
      {
        "id": "db3d1772-c934-47b1-ad28-c7e4582d74e3",
        "first_name": "Frist002",
        "last_name": "Last002",
        "join_time": "2018-03-30T10:55:52.273Z",
        "profile_url": "http://abc.com/uploads/patron/profile/cf2731b3f037e081fee8230378290b62.jpeg",
        "point_balance": 20,
        "prize": "500.0",
        "ranking": 0
      },
      {
        "id": "31f8330c-cf7c-43dc-939c-f00d4c140042",
        "first_name": "Frist001",
        "last_name": "Last001",
        "join_time": "2018-03-30T10:55:52.187Z",
        "profile_url": "http://abc.com/uploads/patron/profile/cf2731b3f037e081fee8230378290b62.jpeg",
        "point_balance": 10,
        "prize": "0.0",
        "ranking": 1
      }
    ]
  }
}
```

This endpoint authenticated by `Manager Token`, and Staff-ID Request Header, staff should be manager staff, and retrieves challenge detail.

### HTTP Request

`GET http://phrenzi.com/api/management/challenges/:challenge_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

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

> if okay, return status coce 200 and `Challenge` objects:

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

> if invalid, return status coce 422 and object:

``` json
{
  "errors": [
    "Start date can't be blank"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and create Challenge

### HTTP Request

`POST http://phrenzi.com/api/management/challenges`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

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

> if okay, return status code 200 and returns `Challenge` object:

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

> if invalid, return status coce 422 and object:

``` json
{
  "errors": [
    "Start date can't be blank"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and update Challenge

### HTTP Request

`PATCH http://phrenzi.com/api/management/challenges/:challenge_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

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

## Current Challenge

```shell
curl "https://phrenzi.com/api/management/challenges/current" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH
```

> If success, return 200 status code with empty response.

``` json
{
  "current_challenge": {
    "id": "c1c68ae5-6d28-407a-bc45-63172927f0f0",
    "start_date": "2018-10-26T16:00:00.000Z",
    "end_date": "2018-10-26T16:00:00.000Z",
    "prize_percentage": "5.0",
    "max_payout_rank": 1,
    "total_sales": "10000.0",
    "ranking": [
      {
        "id": "1ceecdf5-9a56-4826-a4e6-be86b48aea53",
        "first_name": "Frist002",
        "last_name": "Last002",
        "join_time": "2018-10-27T05:14:23.434Z",
        "profile_url": "/uploads/cache/67bd74d470607a07ad4db7c1cdf375e2.jpeg",
        "point_balance": 20,
        "prize": "500.0",
        "ranking": 0
      },
      {
        "id": "948c227e-a536-4d90-910c-525e810fcd7a",
        "first_name": "Frist001",
        "last_name": "Last001",
        "join_time": "2018-10-27T05:14:23.384Z",
        "profile_url": "/uploads/cache/2f7bb57312d3616f3d781b16ba6c2aa0.jpeg",
        "point_balance": 10,
        "prize": "0.0",
        "ranking": 1
      }
    ]
  }
}
```

This endpoint authenticated by `Manager Token`, and Staff-ID Request Header, staff should be manager staff, and retrieves all challenges.

### HTTP Request

`PATCH http://phrenzi.com/api/management/challenges/current`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>
