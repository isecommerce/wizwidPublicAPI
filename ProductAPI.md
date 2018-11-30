# # WIZWID API Documentation


Version 1.0 Alpha

## API Endpoints

### **Product API**

####  POST: http://api.wizwid.com/API/handler/wizwid/kr/Product-AddShopExternal

The Product resource lets you update and create products in a WIZWID's store


To create an Product, do a POST request to the above method with the parameters below.

###### Params

- `Product` 
  - `store_product_id`: **`String`**
  - `name`: **`String`**  (name can not exceed 50 bytes)
  - `description`: **`String`**  (name can not exceed 50 bytes)
  - `original_price`: **`String`**  
  - `offering_price`: **`String`**
  - `url`: **`String`**
  - `image_url`: **`String`**