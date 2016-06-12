# Establishments

## get all establishments

```shell
curl "https://phrenzi.com/api/establishments" \
  -H "Content-Type: application/json" \
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
      "type": "establishments",
      "attributes": {
        "name": "Establishment1",
        "phone": "612345671"
      },
      "relationships": {
        "business-hours": {
          "data": [
            {
              "id": "5ed86971-7126-4223-99fa-cc3344bf5c71",
              "type": "business-hours"
            },
            {
              "id": "dfc808c0-675a-41ba-af94-d36ceddc7b6a",
              "type": "business-hours"
            },
            {
              "id": "e7f5f045-4906-4152-b0ad-2aaf843d51ce",
              "type": "business-hours"
            },
            {
              "id": "fa5accff-06a3-4841-a063-ae455b9dd894",
              "type": "business-hours"
            },
            {
              "id": "ea866513-086c-4074-8344-ec0f4cc940bc",
              "type": "business-hours"
            },
            {
              "id": "e301b703-85d0-4f66-9352-fe2c5217f63e",
              "type": "business-hours"
            },
            {
              "id": "0584f2bd-af9e-4619-9c82-bb3ef86ac06c",
              "type": "business-hours"
            }
          ]
        },
        "address": {
          "data": {
            "id": "68915f71-1e01-4cac-ab38-03a7f68d364a",
            "type": "addresses"
          }
        }
      }
    },
    {
      "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
      "type": "establishments",
      "attributes": {
        "name": "Establishment2",
        "phone": "612345672"
      },
      "relationships": {
        "business-hours": {
          "data": [
            {
              "id": "cb8a21df-391f-4ef6-825a-7cf3fcd62db6",
              "type": "business-hours"
            },
            {
              "id": "1e45e3f4-9655-4596-84cd-e93543acaffd",
              "type": "business-hours"
            },
            {
              "id": "72090844-6cca-44fb-b24e-07a0908715a8",
              "type": "business-hours"
            },
            {
              "id": "aafea676-436b-4c1e-bfcf-27e2c68ff1cd",
              "type": "business-hours"
            },
            {
              "id": "c3a409bd-aaa7-4276-90d2-468953931b01",
              "type": "business-hours"
            },
            {
              "id": "8817d9d5-9851-45a9-ba1e-e313588cd7ce",
              "type": "business-hours"
            },
            {
              "id": "6ba2d2d4-1bbb-492b-a24b-1925fa3dc93e",
              "type": "business-hours"
            }
          ]
        },
        "address": {
          "data": {
            "id": "11b2cdbc-8740-462a-8cc5-dd50393bf23d",
            "type": "addresses"
          }
        }
      }
    }
  ],
  "included": [
    {
      "id": "5ed86971-7126-4223-99fa-cc3344bf5c71",
      "type": "business-hours",
      "attributes": {
        "wday": 0,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "dfc808c0-675a-41ba-af94-d36ceddc7b6a",
      "type": "business-hours",
      "attributes": {
        "wday": 1,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "e7f5f045-4906-4152-b0ad-2aaf843d51ce",
      "type": "business-hours",
      "attributes": {
        "wday": 2,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "fa5accff-06a3-4841-a063-ae455b9dd894",
      "type": "business-hours",
      "attributes": {
        "wday": 3,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "ea866513-086c-4074-8344-ec0f4cc940bc",
      "type": "business-hours",
      "attributes": {
        "wday": 4,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "e301b703-85d0-4f66-9352-fe2c5217f63e",
      "type": "business-hours",
      "attributes": {
        "wday": 5,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "0584f2bd-af9e-4619-9c82-bb3ef86ac06c",
      "type": "business-hours",
      "attributes": {
        "wday": 6,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "68915f71-1e01-4cac-ab38-03a7f68d364a",
      "type": "addresses",
      "attributes": {
        "street1": "MyString",
        "street2": "MyString",
        "city": "MyString",
        "country": "MyString"
      },
      "relationships": {
        "addressable": {
          "data": {
            "id": "a0f96e8b-f0eb-427a-8e76-1e9b3554edc2",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "cb8a21df-391f-4ef6-825a-7cf3fcd62db6",
      "type": "business-hours",
      "attributes": {
        "wday": 0,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "1e45e3f4-9655-4596-84cd-e93543acaffd",
      "type": "business-hours",
      "attributes": {
        "wday": 1,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "72090844-6cca-44fb-b24e-07a0908715a8",
      "type": "business-hours",
      "attributes": {
        "wday": 2,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "aafea676-436b-4c1e-bfcf-27e2c68ff1cd",
      "type": "business-hours",
      "attributes": {
        "wday": 3,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "c3a409bd-aaa7-4276-90d2-468953931b01",
      "type": "business-hours",
      "attributes": {
        "wday": 4,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "8817d9d5-9851-45a9-ba1e-e313588cd7ce",
      "type": "business-hours",
      "attributes": {
        "wday": 5,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "6ba2d2d4-1bbb-492b-a24b-1925fa3dc93e",
      "type": "business-hours",
      "attributes": {
        "wday": 6,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "11b2cdbc-8740-462a-8cc5-dd50393bf23d",
      "type": "addresses",
      "attributes": {
        "street1": "MyString",
        "street2": "MyString",
        "city": "MyString",
        "country": "MyString"
      },
      "relationships": {
        "addressable": {
          "data": {
            "id": "34aade4c-9a11-4f3b-a96f-57b1a73610f0",
            "type": "establishments"
          }
        }
      }
    }
  ]
}
```

This endpoint retrieves all establishments

### HTTP Request

`GET http://example.com/api/establishments`

<aside class="warning">We will add pagination parameter later, but for this phase, we just skip it.</aside>
