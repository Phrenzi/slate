# PatronApp / Invitation

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


## Invitation patron list

```shell
curl "https://phrenzi.com/api/patron_app/boosters/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/patrons" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
```

> if success invited, then returns status code 200 with following json:

```json
{
  "patrons": [
    {
      "id": "644553a9-35ff-4055-b9d5-d53ecc9c8697",
      "name": "David",
      "aasm_state": "waiting"
    },
    {
      "id": "ad94291b-1f2b-4e2f-bdb6-8265ce0ed89f",
      "name": "Kerry",
      "aasm_state": "opened"
    },
    {
      "id": "709eff27-5942-4530-be8d-de0421e61e5f",
      "name": "Peter",
      "aasm_state": "cancelled"
    },
    {
      "id": "e8a89686-84a8-4e65-9712-4be4223bca25",
      "name": "Ryan",
      "aasm_state": "checked_in"
    },
    {
      "id": "db8c75ab-a6e9-47dd-9a51-afc3be2f85c8",
      "name": "Zee",
      "aasm_state": "checked_in"
    }
  ]
}
```

> if booster specify is invalid / expired, return status code 406 and following json message:


```json
{
  "errors": [
    "Booster specify is not active now"
  ]
}
```

This endpoint get a patron list with aasm_state which is related to current login patron.

### HTTP Request

`GET http://example.com/api/patron_app/boosters/:booster_id/patrons`

### Query Parameters
NOTED: booster_id is the uuid of booster, and must be a invitation booster

### Patron Response

returned patron response along with aasm_state, here's a summary of possible values and related description

Parameter | Value | Description
--------- | ----------- | -----------
aasm_state | 'opened' | patron is not invited by current patron, one can call invite api to invite that patron
aasm_state | 'waiting' | patron is invited by current patron, can not invite anymore
aasm_state | 'cancelled' | invitation to that patron is cancelled by current patron in earlier time, one can call invite api to invite that patron again
aasm_state | 'checked_in' | that patron is already checked-in, either invited by current patron or invited by other patrons, can not invite anymore


## Inviter patron list

```shell
curl "https://phrenzi.com/api/patron_app/boosters/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/inviters" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
```

> if success invited, then returns status code 200 with following json:

```json
{
  "patrons": [
    {
      "id": "f0dab179-de3b-486a-87bd-35643242350f",
      "name": "David"
    },
    {
      "id": "d7bb37d4-873b-4b5d-81eb-46bb023a465e",
      "name": "Ryan"
    }
  ]
}
```

> if current login patron is already checked-in ( as a host ), then returns status code 200 with empty arrays:

```json
{
  "patrons": [
  ]
}
```

> if booster specify is invalid / expired, return status code 406 and following json message:


```json
{
  "errors": [
    "Booster specify is not active now"
  ]
}
```

This endpoint get a host list regarding on invitation booster specify

### HTTP Request

`GET http://example.com/api/patron_app/boosters/:booster_id/inviters`

### Query Parameters
NOTED: `booster_id` is the uuid of booster, and must be a invitation booster
