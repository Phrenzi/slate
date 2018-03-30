# Management / Holidays

## Get all holidays

```shell
curl "https://phrenzi.com/api/management/holidays" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -d '{
    "start": "2018-03-01",
    "end": "2018-03-28"
    }'

```

> The above command returns array of `Holiday` objects:

```json
{
  "holidays": [
    {
      "id": "5d76c3ee-193b-4504-bfbf-c19ee217fa19",
      "title": "MyString",
      "start_date": "2018-04-01",
      "end_date": "2018-04-02"
    },
    {
      "id": "39f44649-cb0d-44f3-8e47-a4bfdaa9dd83",
      "title": "MyString",
      "start_date": "2018-04-03",
      "end_date": "2018-04-04"
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and Staff-ID Request Header, staff should be manager staff, and retrieves all holidays.

### HTTP Request

`GET http://phrenzi.com/api/management/holidays`

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

## Create Holiday

```shell
curl "https://phrenzi.com/api/management/holidays" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X POST \
  -d '{
    "start_date": "2018-03-01",
    "end_date": "2018-03-07",
    "title": 'X-Max'
    }'
```

> if okay, return status coce 200 and `Holiday` objects:

```json
{
  "holiday": {
    "id": "3bde6c6c-d856-4ce2-8879-2f8eec024547",
    "title": "X-Max",
    "start_date": "2018-03-01",
    "end_date": "2018-03-07"
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

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and create Holiday

### HTTP Request

`POST http://phrenzi.com/api/management/holidays`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
start_date | Y | start date of holiday
end_date | Y | end date of holiday
title | Y | the title displayed for Holiday

## Update Holiday

```shell
curl "https://phrenzi.com/api/management/holidays/a635683c-87d3-4531-a5b5-f58d44d053b8" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "start_date": "2018-03-01",
    "end_date": "2018-03-07",
    "title": 'X-max'
    }'
```

> if okay, return status code 200 and returns `Holiday` object:

```json
{
  "holiday": {
    "id": "a635683c-87d3-4531-a5b5-f58d44d053b8",
    "title": "X-max
    "start_date": "2018-03-01",
    "end_date": "2018-03-07"
  }
}
```

> if invalid, return status coce 422 and object:

``` json
{
  "errors": [
    "Start date can't be blank",
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and update Holiday

### HTTP Request

`PATCH http://phrenzi.com/api/management/holidays/:holiday_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
start_date | Y | start date of holiday
end_date | Y | end date of holiday
title | Y | the title displayed for Holiday

## Delete Holiday

```shell
curl "https://phrenzi.com/api/management/holidays/a635683c-87d3-4531-a5b5-f58d44d053b8" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X DELETE
```

> If success, return 200 status code with empty response.

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and delete Holiday

### HTTP Request

`DELETE http://phrenzi.com/api/management/holidays/:holiday_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>
