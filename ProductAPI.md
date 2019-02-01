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
curl -H "Content-Type: application/json" -X POST -d 
'{"Product":
	[
		{
			"store_product_id":"11365"
			"name":"Phyliss Heart Pointelle",
			"description":"description TEST",
			"original_price":"253.00",
			"offering_price":"253.00",
			"url":"Product URL",
			"image_url":
				[
					"PRODUCT IMAGE"
				]
			
			"options":
				[
					{
						"option1":"POPPY",
						"option2":"X-SMALL",
						"alt_images":
							[
								"PRODUCT SUB IMAGE URL",
								"PRODUCT SUB IMAGE URL",
								"PRODUCT SUB IMAGE URL"
							]
						,"price":"253.00"
					}
					,{
						"option1":"POPPY",
						"option2":"SMALL",
						"alt_images":
							[
								"PRODUCT SUB IMAGE URL",
								"PRODUCT SUB IMAGE URL",
								"PRODUCT SUB IMAGE URL"
							]
						,"price":"253.00"
					}
				],
			"wizwid_brand_id":"091623",
			"wizwid_category_id":"001105371",
			"wizwid_store_id":"156475"
		}
	]
}'
 http://renewalapi.wizwid.com/API/handler/wizwid/kr/Product-AddShopExternal
```    


