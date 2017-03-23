# PatronApp / Boosters

## get all boosters today

```shell
curl "https://phrenzi.com/api/patron_app/establishments/c3d12f1a-1f0e-4ade-ae6a-49660db2b2ea/boosters" \
  -H "Content-Type: application/json" \
```

> The above command returns JSON structured like this:

```json
{
  "boosters": [
    {
      "id": "74728c5c-bbc1-4212-91e4-037c25eef234",
      "booster_type": "check_in",
      "status": "actived",
      "start_time": "2017-03-22T05:55:39.000Z",
      "point": "100.0",
      "finished_by": "end_time",
      "end_time": "2017-03-22T06:03:59.000Z",
      "patron": {
        "redeemed": false
      }
    },
    {
      "id": "9ecedaf3-9b39-4199-9b8f-b050c144b98d",
      "booster_type": "check_in",
      "status": "finished",
      "start_time": "2017-03-22T05:57:19.000Z",
      "point": "100.0",
      "finished_by": "quantity",
      "quantity": 1,
      "claimed_count": 1,
      "patron": {
        "redeemed": true,
        "check_in_at": "2017-03-22T04:03:12.000Z"
      }
    },
    {
      "id": "f69285c8-0556-4a26-9c53-f0ca8c9e516f",
      "booster_type": "target_amount",
      "start_time": "2017-03-22T05:58:59.000Z",
      "end_time": "2017-03-22T05:59:49.000Z",
      "status": "finished",
      "point": "100.0",
      "target_amount": "100.0",
      "claimed_count": 1,
      "patron": {
        "redeemed": false
      }
    },
    {
      "id": "6c17a61e-c786-4801-aa5c-2965a94b1585",
      "booster_type": "target_amount",
      "start_time": "2017-03-22T06:02:15.000Z",
      "end_time": "2017-03-22T06:03:05.000Z",
      "status": "finished",
      "point": "100.0",
      "target_amount": "100.0",
      "claimed_count": 1,
      "patron": {
        "redeemed": false,
        "number_of_transaction": 1,
        "total_accumulated_sales": "50.0",
        "not_rewarded_sales": "50.0",
        "accumulated_claimed_count": 0
      }
    },
    {
      "id": "bf15f7c5-ddee-404f-9966-c9feaea36b53",
      "booster_type": "target_amount",
      "start_time": "2017-03-22T06:03:12.000Z",
      "end_time": "2017-03-22T06:04:02.000Z",
      "status": "finished",
      "point": "100.0",
      "target_amount": "100.0",
      "claimed_count": 1,
      "patron": {
        "redeemed": true,
        "number_of_transaction": 2,
        "total_accumulated_sales": "150.0",
        "not_rewarded_sales": "50.0",
        "accumulated_claimed_count": 1
      }
    },
    {
      "id": "981a00e6-9dcf-4af0-91a5-74f3f2a81882",
      "booster_type": "invitation",
      "start_time": "2017-03-22T05:59:49.000Z",
      "status": "actived",
      "end_time": "2017-03-22T06:00:49.000Z",
      "host_point": "100.0",
      "invitee_point": "100.0",
      "unlimited": true,
      "claimed_count": 1,
      "patron": {
        "redeemed": false,
        "host_count": 0
      }
    },
    {
      "id": "80284ba8-9e0e-447a-bdb7-5ef6b2187c99",
      "booster_type": "invitation",
      "start_time": "2017-03-22T05:59:59.000Z",
      "status": "finished",
      "end_time": "2017-03-22T06:00:34.000Z",
      "host_point": "100.0",
      "invitee_point": "100.0",
      "unlimited": false,
      "invitation_limit": 2,
      "claimed_count": 1,
      "patron": {
        "redeemed": false,
        "host_count": 2
      }
    },
    {
      "id": "aba9872b-6831-4e7e-ba8e-75b711344ba8",
      "booster_type": "invitation",
      "start_time": "2017-03-23T09:56:53.000Z",
      "status": "actived",
      "end_time": "2017-03-23T09:57:53.000Z",
      "host_point": "100.0",
      "invitee_point": "100.0",
      "unlimited": true,
      "claimed_count": 1,
      "patron": {
        "redeemed": false,
        "check_in_at": "2017-03-23T17:57:43.605+08:00",
        "invitation_sent_count": 2,
        "invited_count": 0,
        "total_claimed_point": "0.0"
      }
    },
    {
      "id": "35a81e59-55eb-4f28-8b2f-7f117f06f938",
      "booster_type": "invitation",
      "start_time": "2017-03-23T09:58:43.000Z",
      "status": "actived",
      "end_time": "2017-03-23T09:59:43.000Z",
      "host_point": "100.0",
      "invitee_point": "100.0",
      "unlimited": true,
      "claimed_count": 1,
      "patron": {
        "redeemed": true,
        "check_in_at": "2017-03-23T17:59:33.185+08:00",
        "invitation_sent_count": 2,
        "invited_count": 1,
        "total_claimed_point": "100.0"
      }
    }
  ]
}
```

This endpoint retrieves all boosters, along with booster information connected with current patron

### HTTP Request

`GET http://example.com/api/patron_app/establishments/:establishment_id/boosters`

<aside class="warning">We will add pagination parameter later, but for this phase, we just skip it.</aside>
