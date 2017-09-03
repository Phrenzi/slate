# PatronApp / Patron Summary

## get patron summary for specify establishment_id

```shell
curl "https://phrenzi.com/api/patron_app/establishments/d51dd6c5-ad0e-445f-b3c5-06ab8ec8624b/summary" \
  -H "Content-Type: application/json" \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com" \
  -d '{
    "establishment_id": "d51dd6c5-ad0e-445f-b3c5-06ab8ec8624b"
    }'
```

> The above command returns JSON structured like this:

```json
{
  "summary": {
    "challenge_played": 10,
    "challenge_won": 5,
    "booster_earned": 2,
    "point_earned": "100.0",
    "prize_earned": "100.0",
    "credit_earned_from_correction": "100.0",
    "credit_loss_from_correction": "100.0",
    "credit_earned_from_cash": "100.0",
    "credit_spent": "100.0",
    "credit_earned_from_deletion": "100.0",
    "credit_loss_from_deletion": "100.0",
    "credit_earned_from_prize": "100.0"
  }
}
```

This endpoint authenticate by patron authenticate, and retrieves summary statistic data for current authenticated patron and for establishment specified

### HTTP Request

`GET http://example.com/api/patron_app/establishments/:establishment_id/summary`
