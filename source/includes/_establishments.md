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
      "id": "68886374-b477-438a-8313-52aed4b55371",
      "type": "establishments",
      "attributes": {
        "name": "Establishment1",
        "phone": "612345671",
        "cash-back": "3.5",
        "desc": "This is an example description",
        "logo-url": "http://example.com/establishment/logo/68886374-b477-438a-8313-52aed4b55371/thumb_image.jpeg",
        "banner-url": "http://example.com/establishment/banner/68886374-b477-438a-8313-52aed4b55371/thumb_image.jpeg"
      },
      "relationships": {
        "business-hours": {
          "data": [
            {
              "id": "99d6dd1e-2009-4353-b4b9-180f5f85d079",
              "type": "business-hours"
            },
            {
              "id": "8d984fee-dcf3-4871-b1ee-a3eb4f71bc17",
              "type": "business-hours"
            },
            {
              "id": "d96678eb-352a-4555-9142-5c563a6d9d65",
              "type": "business-hours"
            },
            {
              "id": "e7218bce-eeb6-49cd-83e4-4ef7a5cc2051",
              "type": "business-hours"
            },
            {
              "id": "a027e983-cb05-4f5a-877f-6ae6ea0f61bd",
              "type": "business-hours"
            },
            {
              "id": "8eee2711-534d-4a29-b6ac-6e42b22239d1",
              "type": "business-hours"
            },
            {
              "id": "6d783fbd-3226-49f7-b063-3ef19d5e2b4d",
              "type": "business-hours"
            }
          ]
        },
        "address": {
          "data": {
            "id": "d0f238f5-34ee-4ad9-81f5-279598568848",
            "type": "addresses"
          }
        }
      }
    },
    {
      "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
      "type": "establishments",
      "attributes": {
        "name": "Establishment2",
        "phone": "612345672",
        "cash-back": "3.5",
        "desc": "This is an example description",
        "logo-url": "http://example.com/establishment/logo/61fd9d4e-236e-44c5-a4da-dc23bd59bc41/thumb_image.jpeg",
        "banner-url": "http://example.com/establishment/banner/61fd9d4e-236e-44c5-a4da-dc23bd59bc41/thumb_image.jpeg"
      },
      "relationships": {
        "business-hours": {
          "data": [
            {
              "id": "bcf85c12-b68a-441c-ab76-68c9d37aebe8",
              "type": "business-hours"
            },
            {
              "id": "a3a36ca2-7bd0-4854-a460-28e867da86c4",
              "type": "business-hours"
            },
            {
              "id": "472e0085-59ef-4af6-bac7-f999bd269198",
              "type": "business-hours"
            },
            {
              "id": "d32f9c15-1066-4e18-b1d3-d6c826f35ea4",
              "type": "business-hours"
            },
            {
              "id": "32714af8-2b6b-4464-a9fc-e203c6fa1537",
              "type": "business-hours"
            },
            {
              "id": "e4f58ea7-3f09-4539-a2c6-306afb44c31c",
              "type": "business-hours"
            },
            {
              "id": "76f720b6-b543-49da-aab0-248ac51811f9",
              "type": "business-hours"
            }
          ]
        },
        "address": {
          "data": {
            "id": "872d4265-b2ee-4434-9dc6-ed8d49ce36d2",
            "type": "addresses"
          }
        }
      }
    }
  ],
  "included": [
    {
      "id": "99d6dd1e-2009-4353-b4b9-180f5f85d079",
      "type": "business-hours",
      "attributes": {
        "wday": 0,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "68886374-b477-438a-8313-52aed4b55371",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "8d984fee-dcf3-4871-b1ee-a3eb4f71bc17",
      "type": "business-hours",
      "attributes": {
        "wday": 1,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "68886374-b477-438a-8313-52aed4b55371",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "d96678eb-352a-4555-9142-5c563a6d9d65",
      "type": "business-hours",
      "attributes": {
        "wday": 2,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "68886374-b477-438a-8313-52aed4b55371",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "e7218bce-eeb6-49cd-83e4-4ef7a5cc2051",
      "type": "business-hours",
      "attributes": {
        "wday": 3,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "68886374-b477-438a-8313-52aed4b55371",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "a027e983-cb05-4f5a-877f-6ae6ea0f61bd",
      "type": "business-hours",
      "attributes": {
        "wday": 4,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "68886374-b477-438a-8313-52aed4b55371",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "8eee2711-534d-4a29-b6ac-6e42b22239d1",
      "type": "business-hours",
      "attributes": {
        "wday": 5,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "68886374-b477-438a-8313-52aed4b55371",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "6d783fbd-3226-49f7-b063-3ef19d5e2b4d",
      "type": "business-hours",
      "attributes": {
        "wday": 6,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "68886374-b477-438a-8313-52aed4b55371",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "d0f238f5-34ee-4ad9-81f5-279598568848",
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
            "id": "68886374-b477-438a-8313-52aed4b55371",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "bcf85c12-b68a-441c-ab76-68c9d37aebe8",
      "type": "business-hours",
      "attributes": {
        "wday": 0,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "a3a36ca2-7bd0-4854-a460-28e867da86c4",
      "type": "business-hours",
      "attributes": {
        "wday": 1,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "472e0085-59ef-4af6-bac7-f999bd269198",
      "type": "business-hours",
      "attributes": {
        "wday": 2,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "d32f9c15-1066-4e18-b1d3-d6c826f35ea4",
      "type": "business-hours",
      "attributes": {
        "wday": 3,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "32714af8-2b6b-4464-a9fc-e203c6fa1537",
      "type": "business-hours",
      "attributes": {
        "wday": 4,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "e4f58ea7-3f09-4539-a2c6-306afb44c31c",
      "type": "business-hours",
      "attributes": {
        "wday": 5,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "76f720b6-b543-49da-aab0-248ac51811f9",
      "type": "business-hours",
      "attributes": {
        "wday": 6,
        "open-time": 39600,
        "close-time": 86400
      },
      "relationships": {
        "establishment": {
          "data": {
            "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
            "type": "establishments"
          }
        }
      }
    },
    {
      "id": "872d4265-b2ee-4434-9dc6-ed8d49ce36d2",
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
            "id": "61fd9d4e-236e-44c5-a4da-dc23bd59bc41",
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
