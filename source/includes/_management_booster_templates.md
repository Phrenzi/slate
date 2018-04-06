# Management / Booster Templates

## Get all booster templates

```shell
curl "https://phrenzi.com/api/management/booster_templates" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
```

> The above command returns array of `BoosterTemplate` objects:

```json
{
  "booster_templates": [
    {
      "id": "768877b9-55fd-4fc0-bc21-4d73d1af6fb6",
      "title": "random title",
      "start_time": 39600,
      "finished_by": "end_time",
      "end_time": 72000,
      "point": 100,
      "booster_type": "check_in"
    },
    {
      "id": "acca7b24-a29f-4143-be85-442f47d0f204",
      "title": "random title",
      "start_time": 39600,
      "finished_by": "end_time",
      "end_time": 72000,
      "point": 100,
      "booster_type": "task",
      "task_desc": "Task desc"
    },
    {
      "id": "b4c2e31e-9e0a-4cb7-a255-875da0877a88",
      "title": "random title",
      "start_time": 39600,
      "end_time": 72000,
      "host_point": 100,
      "invitee_point": 100,
      "unlimited": true,
      "booster_type": "invitation"
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and Staff-ID Request Header, staff should be manager staff, and retrieves all booster templates

### HTTP Request

`GET http://phrenzi.com/api/management/booster_templates`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

<aside class="info">This API support pagination. please refer to <a
href="#link-response-header">Link Response Header section</a></aside>

## Create Booster Templates

```shell
curl "https://phrenzi.com/api/management/booster_templates" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X POST \
  -d '{
    "booster_type": "check_in",
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
  "booster_template": {
    "id": "0d028b17-e0c7-47ee-a951-3884b39e0603",
    "title": "CheckIn and Play",
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
    "Start time can't be blank"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and create Booster Template

### HTTP Request

`POST http://phrenzi.com/api/management/booster_templates`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

### Query Parameters

For CheckIn Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
booster_type | Y | should be 'check_in'
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required. end_time of booster template, it's second to the begining of the day
finished_by | Y | either 'end_time' or 'quantity'
quantity | N | if finished_by is 'quantity', required. the maximum time for redemption.
title | Y | Title of booster template
point | Y | redemption point

For Task Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
booster_type | Y | should be 'task'
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required. end_time of booster template, it's second to the begining of the day
finished_by | Y | either 'end_time' or 'quantity'
quantity | N | if finished_by is 'quantity', required. the maximum time for redemption.
title | Y | Title of booster template
point | Y | redemption point

For Invitation Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
booster_type | Y | should be 'invitation'
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | Y | end_time of booster template, it's second to the begining of the day
host_point | Y | redemption point as a host
invitee_point | Y | redemption point as a invitee
unlimited | Y | either true or false
title | Y | Title of booster template
invitation_limit | N | if unlimited is false, then required. maximum of Invitaiton host can sent

For Tiered Check In Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
booster_type | Y | should be 'tiered_check_in'
finished_by | Y | should be 'end_time' or 'quantity'
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required, specify end_time of booster template, it's second to the begining of the day
quantity | N | if finished_by is 'quantity', required, quantity of booster that can redeemed
point | Y | check-in point
enable_invitation | Y | true or false
host_point | N | if enable_invitation, required, redemption point as a host
invitee_point | N | if enable_invitation, required, redemption point as a invitee
unlimited | N | if enable_invitation, required, either true or false
title | Y | Title of booster template
invitation_limit | N | if unlimited is false, then required. maximum of Invitaiton host can sent

For Target Amount Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
booster_type | Y | should be 'target_amount'
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | Y | end_time of booster template, it's second to the begining of the day
point | Y | redemption point
target_amount | Y | target_amount that patron purchase to redeem the point
title | Y | Title of booster template

## Update Booster Template

```shell
curl "https://phrenzi.com/api/management/booster_templates/a635683c-87d3-4531-a5b5-f58d44d053b8" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X PATCH \
  -d '{
    "start_time": 39600,
    "finished_by": "end_time",
    "end_time": 79200,
    "point": 100,
    "title": "CheckIn and Play"
    }'
```

> if okay, return status code 200 and returns `BoosterTemplate` object:

```json
{
  "booster_template": {
    "id": "a635683c-87d3-4531-a5b5-f58d44d053b8",
    "title": "CheckIn and Play",
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
    "Start time can't be blank"
  ]
}
```

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and update Booster Template

### HTTP Request

`PATCH http://phrenzi.com/api/management/booster_templates/:booster_template_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>

### Query Parameters
For CheckIn Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required. end_time of booster template, it's second to the begining of the day
finished_by | Y | either 'end_time' or 'quantity'
quantity | N | if finished_by is 'quantity', required. the maximum time for redemption.
title | Y | Title of booster template
point | Y | redemption point

For Task Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required. end_time of booster template, it's second to the begining of the day
finished_by | Y | either 'end_time' or 'quantity'
quantity | N | if finished_by is 'quantity', required. the maximum time for redemption.
title | Y | Title of booster template
point | Y | redemption point

For Invitation Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | Y | end_time of booster template, it's second to the begining of the day
host_point | Y | redemption point as a host
invitee_point | Y | redemption point as a invitee
unlimited | Y | either true or false
title | Y | Title of booster template
invitation_limit | N | if unlimited is false, then required. maximum of Invitaiton host can sent

For Tiered Check In Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
finished_by | Y | should be 'end_time' or 'quantity'
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | N | if finished_by is 'end_time', required, specify end_time of booster template, it's second to the begining of the day
quantity | N | if finished_by is 'quantity', required, quantity of booster that can redeemed
point | Y | check-in point
enable_invitation | Y | true or false
host_point | N | if enable_invitation, required, redemption point as a host
invitee_point | N | if enable_invitation, required, redemption point as a invitee
unlimited | N | if enable_invitation, required, either true or false
title | Y | Title of booster template
invitation_limit | N | if unlimited is false, then required. maximum of Invitaiton host can sent

For Target Amount Booster Template

Parameter | Required | Description
--------- | ----------- | ----------
start_time | Y | start time of booster template, it's second to the begining of the day
end_time | Y | end_time of booster template, it's second to the begining of the day
point | Y | redemption point
target_amount | Y | target_amount that patron purchase to redeem the point
title | Y | Title of booster template

*NOTED:*

* booster_type can not been changed

## Delete Booster Template

```shell
curl "https://phrenzi.com/api/management/booster_template/a635683c-87d3-4531-a5b5-f58d44d053b8" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468" \
  -X DELETE
```

> If success, return 200 status code with empty response.

This endpoint authenticated by `Manager Token` ( using Staff-ID Request Header, staff should be manager staff ) and delete Booster Template

### HTTP Request

`DELETE http://phrenzi.com/api/management/booster_templates/:booster_template_id`

<aside class="info">This API require Staff-Id Request Header. please refer to <a
href="#staff-id-request-header">Staff-Id Request Header section</a></aside>
