# Json Objects

normally, a api response in Phrenzi, will be somehow like this in the right hand side :

``` json
{
  "data": {
    "id": "ABCCDD",
    "type": "patrons",
    "attributes": {
      "name": "Simon",
      "email": "abc@example.com",
      "credit-balance": "123.22",
      "trans-code": "asdfw1"
    }
  }
}
```

In `data` tag, it represent the important part for client to consuming, either a json object, or
Array of json objects. It would be easier for us to classify different json object from Phrenzi api
returned, so we list all the different json object here:

For example, the api response on the right hand side represent a `Patron` json object below.

## Patron

Key | Type | Example | Description
--------- | --------- | --------- | -----------
name | String | 'Simon Iong' | the name of Patron
credit-balance | String | '123.22' | the current avaliable balance for Patron
email | String | "abc@example.com" | the email from Patron
trans-code | String | "asdfw1" | 6 digit trans code

## Basic Patron

Key | Type | Example | Description
--------- | --------- | --------- | -----------
name | String | 'Simon Iong' | the name of Patron
credit_balance | String | "123.22" | the current avaliable balance for Patron
trans-code | String | "asdfw1" | 6 digit trans code

## Manager

Key | Type | Example | Description
--------- | --------- | --------- | -----------
name | String | 'Simon Iong' | the name of Manager
email | String | 'abc@example.com' | the email from Manager

## Establishment
Key | Type | Example | Description
--------- | --------- | --------- | -----------
name | String | 'Awesome Bar' | the name of Establishment |
phone | String | '123434123' | the phone contact for Establishment |
desc | String | 'asdfsad' | the desc for Establishment |
cash_back | String | '3.5' | the current cash back setting |
address | Address object | see below | the address object attached to this establishment |
business_hours | Array of Business Hour | see below | totally 7 business hour object |

## Basic Establishment
Key | Type | Example | Description
--------- | --------- | --------- | -----------
name | String | 'Awesome Bar' | the name of Establishment |
phone | String | '123434123' | the phone contact for Establishment |
desc | String | 'asdfsad' | the desc for Establishment |
cash_back | String | '3.5' | the current cash back setting |

## Address
Key | Type | Example | Description
--------- | --------- | --------- | -----------
street1 | String | 'Ma Wan MainRold' | the street1 for Establishment |
street2 | String | 'Ma Wan' | the street2 for Establishment |
city | String | 'Hong Kong' | city for Establishment |
country | String | 'HK' | country name for ISO 3166-1 standard |

## Business Hour
Key | Type | Example | Description
--------- | --------- | --------- | -----------
open_time | Integer | 43200 | the integer represent the seconds start from mid night, range from 0..86400 |
close_time | Integer | 63200 | the integer represent the seconds start from mid night, range from 0..129600, means, until 12pm next day |
wday | Integer | 1 | integer represent the day in the week, 0 for sunday, 1 for monday, etc |
closed | Boolean | false | true/false, true stands for establishment is close this day

## Transaction

Key | Type | Example | Description
--------- | --------- | --------- | -----------
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'sale' | type of transaction, either 'sale', or 'correction' |
sale_amount | String | '200.00' | different meaning for different scenarios |
credit_amount | String | '7.00' | different meaning for different scenarios |
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |

### Scenario 1: fully sale record:

sale amount is 200, cash_back setting is 3.5%, then earned credit 7.00

Key | Type | Example | Description
--------- | --------- | --------- | -----------
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'sale' | type of transaction, either 'sale', or 'credit', or 'correction' |
sale_amount | String | '200.00' | the sale amount of this transaction
credit_amount | String | '7.00' | the credit patron get from this transaction
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |

### Scenario 2: Partially credit redeem:

sale amount is 200, 125 credit redeemed, then sale & credit record would be:

Key | Type | Example | Description
--------- | --------- | --------- | -----------
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'sale' | type of transaction |
sale_amount | String | '75.00' | in this case, we deduct 125 credit |
credit_amount | String | '2.63' | 75 * 0.035 = 2.625
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |

Key | Type | Example | Description
--------- | --------- | --------- | -----------
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'credit' | type of transaction |
sale_amount | String | '125.00' | the sale amount redeem by credit |
credit_amount | String | '-125.00' | the credit deduct from current balance of Patron |
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |

### Scenario 3: Fully credit redeem:

sale amount is 200, 200 credit redeemed, then there is no sale record, only credit record.

Key | Type | Example | Description
--------- | --------- | --------- | -----------
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'credit' | type of transaction |
sale_amount | String | '200.00' | the sale amount redeem by credit |
credit_amount | String | '-200.00' | the credit deduct from current balance of Patron |
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |

### Scenario 3: Credit correct:

manager decide to deduct 200 credit balance for Patron.

Key | Type | Example | Description
--------- | --------- | --------- | -----------
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'correction' | type of transaction |
sale_amount | String | '0.00' | the sale amount redeem by credit |
credit_amount | String | '-200.00' | deduct 200 from system |
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
