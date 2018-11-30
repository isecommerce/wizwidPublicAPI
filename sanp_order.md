# Snapi Documentation

Version 1.0 Alpha (3/07/2017)

## Changelog

## API Endpoints

### **Order API**

####  POST: `https://api.snapi.global/orders.json`

To order an item, do a `POST` request to the above method with the parameters below. 

You can bypass the `expected_prices` check by simply not passing it as a parameter.

##### Headers

- `Authorization`: **`String`** - The auth token for the user. Shown in the Snapi Admin UI.

###### Params

- `expected_prices` (optional) - The prices you expect each to be based on your estimates
  - `item_total`: **`Double`**
  - `local_tax_total`: **`Double`**
  - `local_shipment_total`: **`Double`**
- `order_reference`: **`String`** - An internal reference number
- `order_email`: **`String`** - The email for the order details to be sent to
- `webhook_status_update`: **`String`** - THis URL will be called via a `POST` call with the order status and order reference given
- `affiliate_link`: **`String`** (optional) - The affiliate link to use
- `address` - US Address and name
  - `korean_name`: **`String`** - Preferred, send if you do not have english name
  - `first_name`: **`String`** - optional (English)
  - `last_name`: **`String`** - optional (English)
  - `locker_id`: **`String`**
  - `address`: **`String`**
  - `city`: **`String`**
  - `state`: **`String`**
  - `zip`: **`String`**
  - `phone`: **`String`** - US phone number
- `billing_address` - Card address/name
  - `title`: **`String`** - `Mr.`, `Mrs.` etc
  - `first_name`: **`String`**
  - `last_name`: **`String`**
  - `address`: **`String`**
  - `city`: **`String`**
  - `state`: **`String`**
  - `zip`: **`String`**
  - `phone`: **`String`**
- `product`
  - `selected_options`: **`Hash/Dictionary`** - Hash of the options desired for the product e.g. `{ "color" => "Blue", "size" => "10" }`
  - `url`: **`String`** - URL of the product
- `card_details`
  - `card_type`: **`String`** - The card type, e.g. `Mastercard` or `Visa`
  - `card_name`: **`String`** - Card owner's name
  - `card_number`: **`String`** - Card's number
  - `cvv`: **`String`** - CVV security code of the card
  - `expiry_date_month`: **`String`** - Month in number form e.g. `12`
  - `expiry_date_year`: **`String`** - Year in number form e.g. `2020`
- `login_details`
  - `username`: **`String`** - The username or email to use for Shopbop or other login only sites
  - `password`: **`String`** - Password for above account


##### Errors

- `ExpectedPriceError` - Returns when your expected prices do not match our estimates given the price buffer set in the admin system. Below is the expected error message for this.
  - `"Our estimated total was more than your expected total, your expected prices: {"item_total": 5.0, "local_shipment_total": 0.0, "local_tax_total": 0.0 }, our estimated prices: {"item_total": 10.0, "local_shipment_total": 0.0, "local_tax_total": 0.0 }}`
  
- When given bad options or missing options one of two errors as below may be returned. When this occurs please refer to our coming bookmarklet to continue ordering at this stage.
  - `{"error":"validation_error: Options are ambiguous, more than one variant matches.","code":"error"}` 
  - `{"error":"not_found: Variant matching the selected options not found.","code":"error"}`
  
##### Responses

- `{ "result": "place_started", "actual_prices": {"item_total": 10.0, "local_shipment_total": 0.0, "local_tax_total": 0.0 }, "expected_prices": {"item_total": 10.0, "local_shipment_total": 0.0, "local_tax_total": 0.0 } }` - Successfully began placing the order, updates will be via the webhooks to be added soon.

###### Example CURL request

```
curl -H "Content-Type: application/json" -X POST -d "{ 
  'expected_price': {
    'item_total': 143.0,
    'local_tax_total': 10.0,
    'local_shipment_total': 10.0,
  },
  'order_reference': 'C434743',
  'address': {
    'first_name': 'John',
    'last_name': 'Doe',
    'locker_id': 'C434743', # we could use order_reference here?
    'address': '2344 Main Street',
    'city': 'Portland',
    'state': 'OR',
    'zip': '92703',
    'phone': '500500500',
  },
  'product': {
    "selected_options": { "option": "Default" },
    "url": "https://www.thinkgeek.com/product/iiur/?pfm=HP_ProdTab_2_3_Bestsellers_iiur"
  },
  'card_details': {
    'card_type' : 'Mastercard'
    'card_name': 'Test Name',
    'card_number': '4111111111111111',
    'cvv': '123',
    'expiry_date_month': '12',
    'expiry_date_year': '2020'
  }
}" https://api.snapi.global/orders.json
```

#### Webhooks

Webhooks are HTTP URL callbacks that Snapi uses to give status updates on orders beyond the `place_started` phase. You provide a URL for Snapi to POST to when an order updates.

You can receive webhooks calls for these three events:

- `cancelled` - The order was cancelled and will not be processed
- `external_failed` - The order failed to place with the merchants successfully
- `complete` - The order successfully completed with the merchants

These will come with the order reference you sent on the original call and optionally it may contain the merchant ids of an order (coming soon).

##### Example:

You will pass a URL to the order API under the key `webhook_status_update`. When Snapi gets an order update, we will do a `POST` request with JSON data to this URL to send a payload like the below:

`{ "status": "complete", "order_reference": "c144356", "merchant_order_ids": {"Mac Cosmetics"=>["2622087921", "2622087921", "2622087921"], "Amazon"=>["105-3755027-2643452", "105-3755027-2643452", "105-3755027-2643452"]}}`

Status will match the correct order status from the three available. Orders will also send `merchant_order_ids` where applicable to provide you with the order ids from the merchant sites.