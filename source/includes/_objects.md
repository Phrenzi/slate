# Json Objects

these object will return by apis provided by Phrenzi if needed.

## Patron

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that uniquly represent Patron in Phrenzi
name | String | 'Simon Iong' | the name of Patron
credit_balance | Float | 123.22 | the current avaliable balance for Patron
email | String | 'abc@example.com' | the email from Patron
token | String | 'adafasdszdads' | this is the user token

## Basic Patron

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that uniquly represent Patron in Phrenzi
name | String | 'Simon Iong' | the name of Patron
credit_balance | Float | 123.22 | the current avaliable balance for Patron
email | String | 'abc@example.com' | the email from Patron

## Manager

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that uniquly represent Manager in Phrenzi
name | String | 'Simon Iong' | the name of Manager
email | String | 'abc@example.com' | the email from Manager
token | String | 'adsasdafsdafa' | this is the manager token

## Basic Manager

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that uniquly represent Manager in Phrenzi
name | String | 'Simon Iong' | the name of Manager
email | String | 'abc@example.com' | the email from Manager

## Establishment
Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that uniquly represent Establishment in Phrenzi |
name | String | 'Awesome Bar' | the name of Establishment |
phone | String | '123434123' | the phone contact for Establishment |
address | Address object | see below | the address object attached to this establishment |
business_hours | Array of Business Hour | see below | totally 7 business hour object | 

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
id | String | 'ASDDDD' | the code that unique represent Transaction in Phrenzi |
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'sale' | type of transaction, either 'sale', or 'correction' |
sale_amount | Float | 200.00 | different meaning for different scenarios |
credit_amount | Float | 7.00 | different meaning for different scenarios |

### Scenario 1: fully sale record:

sale amount is 200, cash_back setting is 3.5%, then earned credit 7.00

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that unique represent Transaction in Phrenzi |
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'sale' | type of transaction, either 'sale', or 'credit', or 'correction' |
sale_amount | Float | 200.00 | the sale amount of this transaction
credit_amount | Float | 7.00 | the credit patron get from this transaction

### Scenario 2: Partially credit redeem:

sale amount is 200, 125 credit redeemed, then sale & credit record would be:

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that unique represent Transaction in Phrenzi |
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'sale' | type of transaction |
sale_amount | Float | 75.00 | in this case, we deduct 125 credit |
credit_amount | Float | 2.63 | 75 * 0.035 = 2.625

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that unique represent Transaction in Phrenzi |
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'credit' | type of transaction |
sale_amount | Float | 125.00 | the sale amount redeem by credit |
credit_amount | Float | -125.00 | the credit deduct from current balance of Patron |

### Scenario 3: Fully credit redeem:

sale amount is 200, 200 credit redeemed, then there is no sale record, only credit record.

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that unique represent Transaction in Phrenzi |
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'credit' | type of transaction |
sale_amount | Float | 200.00 | the sale amount redeem by credit |
credit_amount | Float | -200.00 | the credit deduct from current balance of Patron |

### Scenario 3: Credit correct:

manager decide to deduct 200 credit balance for Patron.

Key | Type | Example | Description
--------- | --------- | --------- | -----------
id | String | 'ASDDDD' | the code that unique represent Transaction in Phrenzi |
patron_id | String | 'ADSSDD' | the unique code for Patron this transaction is belongs to |
type | String | 'correction' | type of transaction |
sale_amount | Float | 0.00 | the sale amount redeem by credit |
credit_amount | Float | -200.00 | deduct 200 from system |
