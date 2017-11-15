# Management / Staffs

## Get all staffs

```shell
curl "https://phrenzi.com/api/management/staffs" \
  -H "Content-Type: application/json" \
  -H "Authorization: token"
```

> The above command returns array of `Staff` object like this:

```json
{
  "staffs": [
    {
      "id": "828055eb-a94d-4f71-aa90-110d5b747468",
      "first_name": "first1",
      "last_name": "last1",
      "manager": true,
      "setuped": true
    },
    {
      "id": "10efd10c-22dc-4871-83cc-e8a36c103c85",
      "first_name": "first2",
      "last_name": "last2",
      "manager": false,
      "setuped": false
    }
  ]
}
```

This endpoint authenticated by `Manager Token`, and retrieves all staffs.

### HTTP Request

`GET http://phrenzi.com/api/management/staffs`
