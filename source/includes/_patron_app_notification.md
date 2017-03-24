# PatronApp / Notification

## Subscribe Notification

```shell
curl "https://phrenzi.com/api/patron_app/notification_subscriptions" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
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


This endpoint subscribe current patron to notification pool

### HTTP Request

`POST http://example.com/api/patron_app/notification_subscriptions'

### Query Parameters

Parameter | Required | Description
--------- | ----------- | -----------
device_token | Y | iOS's device token
os_type | Y | Os type, available value are: 'ios', 'android'


## Unsubscribe Notification

```shell
curl "https://phrenzi.com/api/patron_app/notification_subscriptions" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
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


This endpoint unsubscribe current patron from notification pool

### HTTP Request

`DELETE http://example.com/api/patron_app/notification_subscriptions'

### Query Parameters

Parameter | Required | Description
--------- | ----------- | -----------
device_token | Y | iOS's device token
os_type | Y | Os type, available value are: 'ios', 'android'
