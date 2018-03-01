# PatronApp / Friendship

## Send friendship request

```shell
curl "https://phrenzi.com/api/patron_app/friendships" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
  -X POST
  -d '{
    "to_patron_id": "a9ce92dd-1b1d-498a-b7d0-77fffccd20de"
    }'
```

> if okay, return status code 200 and empty json.

> if invited patron is not there, return 422, and json like:

```json
{
  "errors": [
    "Invited Patron is not exist"
  ]
}
```

> if friendship request already been sent out to invited patron, return 422, and json:

```json
{
  "errors": [
    "Invited Patron has already received your friend request, please wait"
  ]
}
```

> if already been friends, return 422, and json:

```json
{
  "errors": [
    "Invited Patron is already your friend"
  ]
}
```

This endpoint authenticated by `Patron Token`, and retrieves all boosters, along with booster information connected with current patron

### HTTP Request

`POST http://example.com/api/patron_app/friendships`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
to_patron_id | Y | Invited Patron's UUID

## Cancel friendship

```shell
curl "https://phrenzi.com/api/patron_app/friendships" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
  -X DELETE
  -d '{
    "to_patron_id": "a9ce92dd-1b1d-498a-b7d0-77fffccd20de"
    }'
```

> If okay, return 200 and empty json.


> If Invited Patron is not ther, return 422, and json:

```json
{
  "errors": [
    "Invited Patron is not exist"
  ]
}
```

> If friendship request send out, but invited patron do not accept/reject it yet, return 422 and json:

```json
{
  "errors": [
    "Invited Patron still not accept your friendship request"
  ]
}
```

> If there's no friendship between current loged in patron & invited patron, return 422 and json:

```json
{
  "errors": [
    "Invited Patron is not your friend"
  ]
}
```

This endpoint authenticated by `Patron Token`, and retrieves all boosters, along with booster information connected with current patron

### HTTP Request

`DELETE http://example.com/api/patron_app/friendship`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
to_patron_id | Y | Invited Patron's UUID


## Accept friendship

```shell
curl "https://phrenzi.com/api/patron_app/friendships/accept" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
  -X POST
  -d '{
    "host_patron_id": "a9ce92dd-1b1d-498a-b7d0-77fffccd20de"
    }'
```

> If okay, return 200 and empty json.


> If Host Patron is not there, return 422, and json:

```json
{
  "errors": [
    "Patron is not exist"
  ]
}
```

> If friendship is already established, return 422 and json:

```json
{
  "errors": [
    "Patron is already your friend"
  ]
}
```

> If host patron do not make any request to current authenticated patron, return 422 and json:

```json
{
  "errors": [
    "Patron do not make a friendship request"
  ]
}
```

This endpoint authenticated by `Patron Token`, and accept friendship request.

### HTTP Request

`POST http://example.com/api/patron_app/friendship/accept`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
host_patron_id | Y | Host Patron's UUID

## Reject friendship

```shell
curl "https://phrenzi.com/api/patron_app/friendships/reject" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
  -X POST
  -d '{
    "host_patron_id": "a9ce92dd-1b1d-498a-b7d0-77fffccd20de"
    }'
```

> If okay, return 200 and empty json.


> If Host Patron is not there, return 422, and json:

```json
{
  "errors": [
    "Patron is not exist"
  ]
}
```

> If there is no friendships, return 422 and json:

```json
{
  "errors": [
    "Patron do not make a friendship request"
  ]
}
```

This endpoint authenticated by `Patron Token`, and reject friendship request.

### HTTP Request

`POST http://example.com/api/patron_app/friendship/reject`

### Query Parameters

Parameter | Required | Description
--------- | ----------- | ----------
host_patron_id | Y | Host Patron's UUID
