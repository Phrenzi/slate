# Management / Boosters

## Get all boosters

```shell
curl "https://phrenzi.com/api/management/boosters" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -d '{
    "start": "2018-03-01",
    "end": "2018-03-28"
    }'

```

> The above command returns array of `Booster` objects:

```json
{
  "boosters": [
    {
      "id": "4a4bd792-d962-4304-bafd-4faccfd5be89",
      "title": "Dummy Title",
      "date": "2018-04-01",
      "start_time": 56686,
      "finished_by": "end_time",
      "end_time": 56888,
      "point": 100,
      "status": "scheduled",
      "booster_type": "task",
      "task_desc": null
    },
    {
      "id": "a9bd28d9-a7a2-44e4-8752-88a154783f1f",
      "title": "Dummy Title",
      "date": "2018-04-03",
      "start_time": 39600,
      "end_time": 72000,
      "host_point": 100,
      "invitee_point": 100,
      "unlimited": true,
      "status": "scheduled",
      "booster_type": "invitation"
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and Staff-ID Request Header, staff should be manager staff, and retrieves all boosters within range.

### HTTP Request

`GET http://phrenzi.com/api/management/boosters`

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

## Create Boosters

```shell
curl "https://phrenzi.com/api/management/booster" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X POST \
  -d '{
    "booster_type": "check_in",
    "date": "2018-03-01",
    "start_time": 39600,
    "finished_by": "end_time",
    "end_time": 79200,
    "point": 100,
    "title": "CheckIn and Play"
    }'
```

> if okay, return status coce 200 and `Booster` objects:

``` json
{
  "booster": {
    "id": "0d028b17-e0c7-47ee-a951-3884b39e0603",
    "title": "CheckIn and Play",
    "date": "2018-04-01",
    "start_time": 46800,
    "finished_by": "end_time",
    "end_time": 54000,
    "point": 100,
    "status": "scheduled",
    "booster_type": "check_in"
  }
}
```

> if invalid, return status coce 422 and object:

``` json
{
  "errors": [
    "Date can't be blank"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and create Booster

### HTTP Request

`POST http://phrenzi.com/api/management/boosters`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

For CheckIn Booster

Parameter | Required | Description
--------- | ----------- | ----------
date | Y | date of booster
booster_type | Y | should be 'check_in'
start_time | Y | start time of booster, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required. end_time date of booster, it's second to the begining of the day
finished_by | Y | either 'end_time' or 'quantity'
quantity | N | if finished_by is 'quantity', required. the maximum time for redemption.
title | Y | Title of booster
point | Y | redemption point

For Task Booster

Parameter | Required | Description
--------- | ----------- | ----------
date | Y | date of booster
booster_type | Y | should be 'task'
start_time | Y | start time of booster, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required. end_time date of booster, it's second to the begining of the day
finished_by | Y | either 'end_time' or 'quantity'
quantity | N | if finished_by is 'quantity', required. the maximum time for redemption.
title | Y | Title of booster
point | Y | redemption point

For Invitation Booster

Parameter | Required | Description
--------- | ----------- | ----------
date | Y | date of booster
booster_type | Y | should be 'invitation'
start_time | Y | start time of booster, it's second to the begining of the day
end_time | Y | end_time date of booster, it's second to the begining of the day
host_point | Y | redemption point as a host
invitee_point | Y | redemption point as a invitee
unlimited | Y | either true or false
title | Y | Title of booster
invitation_limit | N | if unlimited is false, then required. maximum of Invitaiton host can sent

For Target Amount Booster

Parameter | Required | Description
--------- | ----------- | ----------
date | Y | date of booster
booster_type | Y | should be 'target_amount'
start_time | Y | start time of booster, it's second to the begining of the day
end_time | Y | end_time date of booster, it's second to the begining of the day
point | Y | redemption point
target_amount | Y | target_amount that patron purchase to redeem the point
title | Y | Title of booster

## Update Challenge

```shell
curl "https://phrenzi.com/api/management/boosters/a635683c-87d3-4531-a5b5-f58d44d053b8" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "date": "2018-03-01",
    "start_time": 39600,
    "finished_by": "end_time",
    "end_time": 79200,
    "point": 100,
    "title": "CheckIn and Play"
    }'
```

> if okay, return status code 200 and returns `Booster` object:

```json
{
  "booster": {
    "id": "a635683c-87d3-4531-a5b5-f58d44d053b8",
    "title": "CheckIn and Play",
    "date": "2018-04-01",
    "start_time": 39600,
    "finished_by": "end_time",
    "end_time": 79200,
    "point": 100,
    "status": "scheduled",
    "booster_type": "check_in"
  }
}
```

> if invalid, return status coce 422 and object:

``` json
{
  "errors": [
    "Date can't be blank"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and update Booster

### HTTP Request

`PATCH http://phrenzi.com/api/management/boosters/:booster_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters
For CheckIn Booster

Parameter | Required | Description
--------- | ----------- | ----------
date | Y | date of booster
start_time | Y | start time of booster, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required. end_time date of booster, it's second to the begining of the day
finished_by | Y | either 'end_time' or 'quantity'
quantity | N | if finished_by is 'quantity', required. the maximum time for redemption.
title | Y | Title of booster
point | Y | redemption point

For Task Booster

Parameter | Required | Description
--------- | ----------- | ----------
date | Y | date of booster
start_time | Y | start time of booster, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required. end_time date of booster, it's second to the begining of the day
finished_by | Y | either 'end_time' or 'quantity'
quantity | N | if finished_by is 'quantity', required. the maximum time for redemption.
title | Y | Title of booster
point | Y | redemption point

For Invitation Booster

Parameter | Required | Description
--------- | ----------- | ----------
date | Y | date of booster
start_time | Y | start time of booster, it's second to the begining of the day
end_time | Y | end_time date of booster, it's second to the begining of the day
host_point | Y | redemption point as a host
invitee_point | Y | redemption point as a invitee
unlimited | Y | either true or false
title | Y | Title of booster
invitation_limit | N | if unlimited is false, then required. maximum of Invitaiton host can sent

For Target Amount Booster

Parameter | Required | Description
--------- | ----------- | ----------
date | Y | date of booster
start_time | Y | start time of booster, it's second to the begining of the day
end_time | Y | end_time date of booster, it's second to the begining of the day
point | Y | redemption point
target_amount | Y | target_amount that patron purchase to redeem the point
title | Y | Title of booster

*NOTED:*

* If booster status is 'actived', nothing can be updated
* booster_type can not been changed

## Delete Challenge

```shell
curl "https://phrenzi.com/api/management/booster/a635683c-87d3-4531-a5b5-f58d44d053b8" \
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
    "can not delete booster that is already been actived"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and delete Booster

### HTTP Request

`DELETE http://phrenzi.com/api/management/boosters/:booster_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

## Stop Challenge

```shell
curl "https://phrenzi.com/api/management/boosters/a635683c-87d3-4531-a5b5-f58d44d053b8/stop" \
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
    "can not stop booster that is not active"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and stop Challenge

### HTTP Request

`PATCH http://phrenzi.com/api/management/boosters/:booster_id/stop`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>
