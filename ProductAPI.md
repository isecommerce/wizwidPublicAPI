# # WIZWID API Documentation


Version 1.0 Alpha

## API Endpoints

### **Product API**

####  Product ADD POST: http://api.wizwid.com/API/handler/wizwid/kr/Product-AddShopExternal

The Product resource lets you update and create products in a WIZWID's store


To create an Product, do a POST request to the above method with the parameters below.

1. WIZWID Category must be mapped
   - http://api.wizwid.com/API/handler/wizwid/kr/Category-Search
2. WIZWID Brand must be mapped
   -  http://api.wizwid.com/API/handler/wizwid/kr/Brand-Search
   
###### Params

- `Product` 
  - `store_product_id`: **`String`**
  - `name`: **`String`**  (name can not exceed 50 bytes)
  - `description`: **`String`**  
  - `original_price`: **`String`**  
  - `offering_price`: **`String`**
  - `url`: **`String`**
  - `image_url`: **`String`**
  - `wizwid_category_id`: **`String`**
  - `wizwid_brand_id`: **`String`**
  
- `options`   
  - `option1`: **`String`**
  - `option2`: **`String`**
  - `alt_images`: **`String`**
  
  
##### Responses

- `:[{"store_product_id":"17349","RESULTCODE":"0000","MESSAGE":"SUCESS","ASSORT_ID":"WIZWID_PRODCUT_ID"}]`   
    
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