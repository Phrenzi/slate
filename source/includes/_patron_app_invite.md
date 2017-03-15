# PatronApp / Invite Patron

## Invite Patron

```shell
curl "https://phrenzi.com/api/patron_app/boosters/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/invite" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -X POST \
  -d '{
    "invitee_patron_id": "202f96fb-1536-43fa-a6ba-7b0387e90465"
    }'
```

> if success invited, then returns status code 200 with empty body.

> if there's validation error, then return status code 422, and following error JSON
> response, with error explaination:

```json
{
  "errors": { "invitee_patron_id": ["does not exist"] }
}
```

> If current authenticated patron is not checked-in, then he is not allow to invite, in this case, return status code 406 and following
> JSON response:

```json
{
  "errors": ["Can't invite anyone before your check-in"]
}
```

> If invitee is already invited, return status code 406 and following JSON response:

```json
{
  "errors": ["Invitee have been invited"]
}
```

> If invitee already checked-in, return status code 406 and following JSON response:

```json
{
  "errors": ["Invitee already checked-in"]
}
```

> If host reach invitation limit, return status code 406 and following JSON response:

```json
{
  "errors": ["You have reached invitation limit, can't invite anymore"]
}
```

This endpoint create a invitation for current logined patron to patron specify

### HTTP Request

`POST http://example.com/api/patron_app/boosters/:booster_id/invite`

### Query Parameters

NOTED: booster_id is the uuid of booster, and must be a invitation booster

Parameter | Required | Description
--------- | ----------- | -----------
invitee_patron_id | Y | invitee's uuid
