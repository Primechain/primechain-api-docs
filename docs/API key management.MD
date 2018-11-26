## API key management


[1. Create a new API key](#1-create-a-new-api-key)

[2. Passing the API key](#2-passing-the-api-key)

### 1. Create a new API key
To create a new api key, use `post /api/v1/get_api_key` and pass 4 parameters - `first_name`, `last_name`, `email`, `phone` and `company_name`.
```
{
  "first_name": "Rohas",
  "last_name": "Nagpal",
  "email": "rohasnagpal@gmail.com",
  "phone": "0123456789",
  "company_name": "Primechain Technologies"
}
```
```
{
"status": 200,
"api_key": "PT-21fh%Am80RegGMXUWbeELHixML1B0k8I4*0uxPR%wyj8-Im*OFpwRRxbHBU%-Obq"
}
```
***Note:*** The API key is never displayed again.
 
### 2. Passing the API key
The API key should be passed in the `Authorization` header.
![Search](http://www.primechaintech.com/img/api_documentation/authorization_get.png)
![Search](http://www.primechaintech.com/img/api_documentation/authorization_post.png)
