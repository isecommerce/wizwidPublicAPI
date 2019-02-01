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
  
  Without the option 
   - `option`: **`String`** (value:Default} ex)  "options":[{option:"Default"}]	
  
##### Responses

- `:[{"store_product_id":"17349","RESULTCODE":"0000","MESSAGE":"SUCESS","ASSORT_ID":"WIZWID_PRODCUT_ID"}]`   
    
###### Example  request

```
{
	"Product":
		[{
			"store_product_id":"123456789",
	 		"name":"Co. Women's Westlyn Penny Loafer",
	 		"description":"<p style=\"color:red;\"> Product Description </p>",
	 		"original_price":"30.4",
	 		"offering_price":"29.5",
	 		"url":"https://www.backcountry.com/patagonia-retro-fleece-vest-boys?skid=PAT00KN-NATGNA-XS&ti=U2VhcmNoIFJlc3VsdHM6UmV0cm8tWDoxOjE1OlJldHJvLVg=",
	 		"image_url":["http://www.img.com/test.jpg",	"http://www.img.com/test1.jpg"],
	 		"wizwid_category_id":"001088842",
	 		"wizwid_brand_id":"000000",
	 		"wizwid_store_id":"101834",
			"options":[{color:RED,size:M,image:http://xxx.xxx.com/img},{color:RED,size:L,image:http://xxx.xxx.com/img},{color:BLUE,size:M,image:http://xxx.xxx.com/img}]
	 	}]
}


```    


