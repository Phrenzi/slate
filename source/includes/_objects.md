# JSON Objects

normally, a api response in Phrenzi, will be somehow like this in the right hand side :

``` json
{
  "object_name": {
    "object_attribute_a": "ABCCDD",
    "object_attribute_b": "Simon",
    "object_attribute_c": "abc@exmaple.com",
    "object_attribute_d": "1234.22"
    }
}
```

In `object_name` tag, it represent the important part for client to consuming, either a json object, or
Array of json objects. It would be easier for us to classify different json object from Phrenzi api
returned, so we list all the different json object here:

## Patron

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'ddbd0c3c-404d-4ce1-9042-9baecb4ef585' | uniq identifier of Patron
name | String | 'Simon Iong' | the name of Patron
email | String | "abc@example.com" | the email from Patron
credit_balance | String | '123.22' | the current avaliable balance by Patron & Establishment
trans_code | String | "asdfw1" | 6 digit trans code, unique identifier for Patron

Noted that for every patron, could have different credit_balance in different Establishment

## Manager

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'ddbd0c3c-404d-4ce1-9042-9baecb4ef585' | uniq identifier of Manager
name | String | 'Simon Iong' | the name of Manager
email | String | 'abc@example.com' | the email from Manager
establishment_name | String | 'Awesome Bar' | the establishment name of this Manager

## Establishment
Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'ddbd0c3c-404d-4ce1-9042-9baecb4ef585' | uniq identifier of Establishment
name | String | 'Awesome Bar' | the name of Establishment |
phone | String | '123434123' | the phone contact for Establishment |
cash_back | String | '3.5' | the current cash back setting |
desc | String | 'asdfsad' | the desc for Establishment |
logo_url | String | 'http://abc.com/logo.img' | logo url |
banner_url | String | 'http://abc.com/banner.img' | logo url |
location | Location object | see below | the location object attached to this establishment |
business_hours | Array of Business Hour | see below | totally 7 business hour object |

## Location
Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'ddbd0c3c-404d-4ce1-9042-9baecb4ef585' | uniq identifier of Location
name | String | 'Little Mario' | the name of Location |
desc | String | 'Ma Wan' | the description for Location |
lat | String | 1.23232 | latitude for location |
long | String | 1.2323 | longtitude for location |

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
id | UUID | 'ddbd0c3c-404d-4ce1-9042-9baecb4ef585' | uniq identifier of Transaction
patron_id | UUID | 'eebd0c3c-404d-4ce1-9042-9baecb4ef585' | UUID for patron |
establishment_id | UUID | 'ffbd0c3c-404d-4ce1-9042-9baecb4ef585' | UUID for establishment |
challenge_id | UUID | 'ffbd0c3c-404d-4ce1-9042-9baecb4ef585' | UUID for challenge, can be NILL |
type | String | 'sale' | type of transaction, either 'sale', or 'credit', or 'correction' |
sale_amount | String | '200.00' | different meaning for different scenarios |
applied_credit | String | '7.00' | the applied credit to used from credit account |
sales_credit | String | '7.00' | the cash-back from sales_amount |
credit_subtotal | String | '7.00' | sales_credit - applied_credit |
remaining_credit | String | '7.00' | at the timing of create transaction, the credit_balance in credit account |
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted | Boolean | true | true means this transaction is already been deleted |
deleted_at | Datetime | "2016-06-05T07:48:56.050Z" | ISO_8601 format datetime string, the timestamp that this transaction is being deleted |
del_transaction_id | UUID | "ggbd0c3c-404d-4ce1-9042-9baecb4ef585" | UUID of origin delete transaction |
action | String | 'Cash Purchase' | action name for transaction |

NOTED:

* if a transaction A is deleted by api, then a reverted transaction B is created. Both transaction A & B exists in Database, transaction A is called `origin deleted transaction`, transaction B is called `reverted deleted transaction`
* server response json object order by tracked_at descending order.
* Client identify `reverted deleted transaction` by `deleted_at`.
    * If transaction `deleted_at` is present, means that this transaction is `reverted deleted transaction`, one can reference `origin deleted transaction` by `del_transaction_id`
    * `reverted deleted transaction` and `origin deleted transaction` have the same `tracked_at`
    * If `deleted_at` is populated, then `deleted` should be true
    * if `deleted_at` is populated, and client need to display datetime of this record somewhere, then should use `deleted_at` instead of `tracked_at`.
* if transaction `deleted` is false, means client call `delete transaction` api to delete this transaction

### Scenario 1: fully sale record:

sale amount is 200, cash_back setting is 3.5%, then earned credit 7.00

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcd' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'sale' | type of transaction, either 'sale', or 'credit', or 'correction' |
sale_amount | String | '200.00' | the sale amount of this transaction
applied_credit | String | '0.00' | the applied credit from credit account
sales_crecit | String | '7.00' | the credit patron get from this transaction
credit_subtotal | String | '7.00' | total credit earned from this transaction
remaining_credit | String | '7.00' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | null | |
deleted | Boolean | false | |
del_transaction_id | UUID | null | |
action | String | 'Cash Purchase' |

### Scenario 2: Partially credit redeem:

sale amount is 200, 125 credit redeemed, then sale & credit record would be:

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcde' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'sale' | type of transaction |
sale_amount | String | '75.00' | in this case, we deduct 125 credit |
applied_credit | String | '0.00' | the applied credit from credit account
sales_crecit | String | '2.6' | 75 * 0.035 = 2.625 ~> 2.6
credit_subtotal | String | '2.6' | total credit earned from this transaction
remaining_credit | String | '202.60' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | null | |
deleted | Boolean | false | |
del_transaction_id | UUID | null | |
action | String | 'Cash Purchase' |

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcdf' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'credit' | type of transaction |
sale_amount | String | '125.00' | the sale amount redeem by credit |
applied_credit | String | '-125.00' | the applied credit from credit account
sales_crecit | String | '4.4' | 125 * 0.035 = 4.375 ~> 4.4
credit_subtotal | String | '-120.6' | total credit earned from this transaction
remaining_credit | String | '82.00' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | null | |
deleted | Boolean | false | |
del_transaction_id | UUID | null | |
action | String | 'Credit Purchase' |

### Scenario 3: Fully credit redeem:

sale amount is 200, 200 credit redeemed, then there is no sale record, only credit record.

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcdg' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'credit' | type of transaction |
sale_amount | String | '200.00' | the sale amount redeem by credit |
applied_credit | String | '-200.00' | the applied credit from credit account
sales_crecit | String | '7.0' | 200 * 0.035 = 7
credit_subtotal | String | '-193.0' | total credit earned from this transaction
remaining_credit | String | '7.00' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | null | |
deleted | Boolean | false | |
del_transaction_id | UUID | null | |
action | String | 'Credit Purchase' |

### Scenario 4: Credit correct:

manager decide to deduct 200 credit balance for Patron.

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcdh' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'correction' | type of transaction |
sale_amount | String | '0.00' | the sale amount redeem by credit |
applied_credit | String | '0.00' | the applied credit from credit account
sales_crecit | String | '0.0' | cash-back generated from sales_amount
credit_subtotal | String | '-200.00' | total credit earned from this transaction
remaining_credit | String | '100.00' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | null | |
deleted | Boolean | false | |
del_transaction_id | UUID | null | |
action | String | 'Credit Correciton' |

### Scenario 5: Delete Full Sale Record from Scenario 1 

Original Sale transaction

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcd' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'sale' | type of transaction, either 'sale', or 'credit', or 'correction' |
sale_amount | String | '200.00' | the sale amount of this transaction
applied_credit | String | '0.00' | the applied credit from credit account
sales_crecit | String | '7.00' | the credit patron get from this transaction
credit_subtotal | String | '7.00' | total credit earned from this transaction
remaining_credit | String | '7.00' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | null | |
deleted | Boolean | false | |
del_transaction_id | UUID | null | |
action | String | 'Cash Purchase' |

Reverted Sale transaction

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcd2' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'sale' | type of transaction, either 'sale', or 'credit', or 'correction' |
sale_amount | String | '-200.00' | the sale amount of this transaction
applied_credit | String | '0.00' | the applied credit from credit account
sales_crecit | String | '-7.00' | the credit patron get from this transaction
credit_subtotal | String | '-7.00' | total credit earned from this transaction
remaining_credit | String | '100.00' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | "2016-06-05T07:48:56.050Z" | |
deleted | Boolean | true | |
del_transaction_id | UUID | "abcd" | |
action | String | 'Cash Purchase Deletion' |

### Scenario 6: Delete Partial Sale Record from Scenario 2

Original Sale Transaction

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcde' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'sale' | type of transaction |
sale_amount | String | '75.00' | in this case, we deduct 125 credit |
applied_credit | String | '0.00' | the applied credit from credit account
sales_crecit | String | '2.6' | 75 * 0.035 = 2.625 ~> 2.6
credit_subtotal | String | '2.6' | total credit earned from this transaction
remaining_credit | String | '202.60' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | null | |
deleted | Boolean | false | |
del_transaction_id | UUID | null | |
action | String | 'Cash Purchase' |

Original Credit Transaction

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcdf' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'credit' | type of transaction |
sale_amount | String | '125.00' | the sale amount redeem by credit |
applied_credit | String | '-125.00' | the applied credit from credit account
sales_crecit | String | '4.4' | 125 * 0.035 = 4.375 ~> 4.4
credit_subtotal | String | '-120.6' | total credit earned from this transaction
remaining_credit | String | '82.00' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | null | |
deleted | Boolean | false | |
del_transaction_id | UUID | null | |
action | String | 'Credit Purchase' |

Reverted Sale transaction

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcde2' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'sale' | type of transaction |
sale_amount | String | '-75.00' | in this case, we deduct 125 credit |
applied_credit | String | '0.00' | the applied credit from credit account
sales_crecit | String | '-2.6' | 75 * 0.035 = 2.625 ~> 2.6
credit_subtotal | String | '-2.6' | total credit earned from this transaction
remaining_credit | String | '152.6' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | "2016-06-05T07:48:56.050Z" | |
deleted | Boolean | true | |
del_transaction_id | UUID | 'abcde' | |
action | String | 'Cash Purchase Deletion' |

Reverted Credit transaction

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | UUID | 'abcdf2' | UUID of transaction |
patron_id | UUID | 'ADSSDD' | UUID of patron |
establishment_id | UUID | 'ADSSDD' | UUID of establishment |
type | String | 'credit' | type of transaction |
sale_amount | String | '-125.00' | the sale amount redeem by credit |
applied_credit | String | '125.00' | the applied credit from credit account
sales_crecit | String | '-4.4' | 125 * 0.035 = 4.375 ~> 4.4
credit_subtotal | String | '120.6' | total credit earned from this transaction
remaining_credit | String | '273.2' | after create this transaction, total balance in credit account
tracked_at | Datetime | "2016-06-04T07:48:56.050Z" | ISO_8601 format datetime string |
deleted_at | Datetime | "2016-06-05T07:48:56.050Z" | |
deleted | Boolean | true | |
del_transaction_id | UUID | 'abcdf' | |
action | String | 'Credit Purchase Deletion' |
