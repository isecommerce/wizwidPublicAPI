# # WIZWID API Documentation


Version 1.0 Alpha

## API Endpoints

### **Product API**

####  POST: http://api.wizwid.com/API/handler/wizwid/kr/Product-AddShopExternal

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
    