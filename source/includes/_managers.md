# Managers

## Login

```shell
curl "https://phrenzi.com/api/v1/managers/sign_in"
  -H "Authorization: your_token"
  -X POST
  -d '{
        "email": "abc@gmail.com",
        "password": "password" }'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`POST http://example.com/api/v1/patron/sign_in`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
email | N/A | the email of patron account
password | N/A | the password of patron account

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>
