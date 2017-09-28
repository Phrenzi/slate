# PatronApp / Notification

## Notification List
```shell
curl "https://phrenzi.com/api/patron_app/notification_subscriptions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
```

> if success then returns status code 200 with subscriptions detail objects.


```json
{
  "subscriptions": [
    {
      "device_token": "b62efad0-5ae8-42c7-b11b-860ae3078952",
      "os_type": "ios",
      "subscribed_at": "2017-04-13T10:02:49.575Z"
    },
    {
      "device_token": "38cbc5fe-d051-4015-b8dc-7857334c61b5",
      "os_type": "android",
      "subscribed_at": "2017-04-13T10:04:29.575Z"
    }
  ]
}
```

This endpoint authenticate by `Patron Token` and return all subscriptions record for current patron

### HTTP Request

`GET http://example.com/api/patron_app/notification_subscriptions`

## Subscribe Notification

```shell
curl "https://phrenzi.com/api/patron_app/notification_subscriptions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X POST \
  -d '{
    "device_token": "202f96fb-1536-43fa-a6ba-7b0387e90465",
    "os_type": 'ios'
    }'
```

> if success subscribed, then returns status code 200 with empty body.

> if there's validation error, then return status code 422, and following error JSON
> response, with error explaination:

```json
{
  "errors": ["Os type is not included in the list"]
}
```

> If current patron is subscribed already, still return status code 200 with empty body.


This endpoint authenticate by `Patron Token` and subscribe current patron to notification pool

### HTTP Request

`POST http://example.com/api/patron_app/notification_subscriptions`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | -----------
device_token | Y | iOS's device token
os_type | Y | Os type, available value are: 'ios', 'android'


## Unsubscribe Notification

```shell
curl "https://phrenzi.com/api/patron_app/notification_subscriptions" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -X DELETE \
  -d '{
    "device_token": "202f96fb-1536-43fa-a6ba-7b0387e90465",
    "os_type": 'ios'
    }'
```

> if success unsubscribed, then returns status code 200 with empty body.

> if there's validation error, then return status code 422, and following error JSON
> response, with error explaination:

```json
{
  "errors": ["Os type is not included in the list"]
}
```

> If current patron not subscribed before, still return status code 200 with empty body.


This endpoint authenticate by `Patron Token` and unsubscribe current patron from notification pool

### HTTP Request

`DELETE http://example.com/api/patron_app/notification_subscriptions`


### Query Parameters

Parameter | Required | Description
--------- | ----------- | -----------
device_token | Y | iOS's device token
os_type | Y | Os type, available value are: 'ios', 'android'
