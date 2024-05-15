<div align="center">
<img src="./assets/Pocket.png" width="200"/>
<h1>PocketBase</h1>
📅 Creation Date: May 09
♾️ Last Update:  
</div>
 
## Index


- [Description](#🎯-description)   
- [Deployment](#💽-deployment) 
- [Project Organization](#📁-project-organization)
- [Endpoints and Request Methods](#📤-endpoints-and-request-methods)
- [Technologies](#✨-technologies)


  

# 🎯 Description

This project aims to understand how PocketBase works, test the types of endpoints it provides, and explore the interface for managing the project.
 

# 💽 Deployment

<h3> Start proyect Windows </h3> 
 
- Open the PocketBase program to see the commands you can execute. 
```bash
./pocketbase.exe
```   
 
- To start the server, you have to use the following command. 
```bash
./pocketbase.exe serve
```   
- Which should output something like the following:
```bash
2024/05/10 10:55:21 Server started at http://127.0.0.1:8090
├─ REST API: http://127.0.0.1:8090/api/
└─ Admin UI: http://127.0.0.1:8090/_/
```   
<h4> 💡 Rutas</h4> 
  
`Server` This is the main HTTP address where the project should be configured. <br>
`REST API` This is the HTTP address where client applications can interact. <br> 
`Admin UI` This is the address where the administration panel provided by PocketBase is located.  

# 📁​ Project organization  

The project organization is very easy to understand, where: 

- In the `Server` This is the main HTTP address where the project should be configured. <br>
- In the `REST API` This is the HTTP address where client applications can interact. <br> 
- In the `Admin UI` This is the address where the administration panel provided by PocketBase is located.

# 📤​ Endpoints and Request Methods 
   
 
- List/Search (products) `get`   
 
Fetch a paginated products records list, supporting sorting and filtering.  
 
```bash
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');

...

// fetch a paginated records list
const resultList = await pb.collection('products').getList(1, 50, {
    filter: 'created >= "2022-01-01 00:00:00" && someField1 != someField2',
});

// you can also fetch all records at once via getFullList
const records = await pb.collection('products').getFullList({
    sort: '-created',
});

// or fetch only the first record that matches the specified filter
const record = await pb.collection('products').getFirstListItem('someField="test"', {
    expand: 'relField1,relField2.subRelField',
});
``` 
 
API details  

```bash
/api/collections/products/records
```    
 
- View (products) `get`   
 
Fetch a single products record.  
 
```bash
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');

...

const record = await pb.collection('products').getOne('RECORD_ID', {
    expand: 'relField1,relField2.subRelField',
});
``` 
 
API details  

```bash
/api/collections/products/records/:id
```    
 
- Create (products) `post`   
 
Create a new products record. <br> 
Body parameters could be sent as `application/json` or `multipart/form-data`. <br>
File upload is supported only via `multipart/form-data`. 
 
```bash
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');

...

// example create data
const data = {
    "name": "test",
    "description": "test",
    "price": 123
};

const record = await pb.collection('products').create(data);
``` 
 
API details  

```bash
/api/collections/products/records
```   
Body Parameters 

| Field        | Type     | Description                                          | Required/Optional  |
|--------------|----------|------------------------------------------------------|--------------------|
| id           | `String`   | 15-character string to store as record ID.           |  `Optional`           |
|              |          | If not set, it will be auto-generated.               |                    |
| name         | `String`    | Plain text value.                                    |  `Required`           |
| description  | `String`   | Plain text value.                                    | `Required`           |
| image        | `File`      | File object.                                         | `Optional`           |
|              |          | Set to `null` to delete already uploaded file(s).      |                    |
| price        | `Number`    | Number value.                                        | `Required`           |

 
- Update (products) `patch`   
 
Create a new products record. <br> 
Body parameters could be sent as `application/json` or `multipart/form-data`. <br>
File upload is supported only via `multipart/form-data`.   
 
```bash
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');

...

// example update data
const data = {
    "name": "test",
    "description": "test",
    "price": 123
};

const record = await pb.collection('products').update('RECORD_ID', data);
``` 
 
API details  

```bash
/api/collections/products/records
```     
 
Body Parameters 

| Field        | Type     | Description                                          | Required/Optional  |
|--------------|----------|------------------------------------------------------|--------------------|
| id           | `String`   | 15-character string to store as record ID.           |  `Optional`           |
|              |          | If not set, it will be auto-generated.               |                    |
| name         | `String`    | Plain text value.                                    |  `Required`           |
| description  | `String`   | Plain text value.                                    | `Required`           |
| image        | `File`      | File object.                                         | `Optional`           |
|              |          | Set to `null` to delete already uploaded file(s).      |                    |
| price        | `Number`    | Number value.                                        | `Required`           |  
 
- Delete (products) `delete`   
 
Delete a single products record.   
 
```bash
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');

...

await pb.collection('products').delete('RECORD_ID');
``` 
 
API details  

```bash
/api/collections/products/records/:id
```     
 
| Field        | Type     | Description                     |
|--------------|----------|---------------------------------|
| id           | `String`   | ID of the record to delete.    |


   
# ✨ Technologies
This project made use of the following technologies: 
  

| Technology         | Logo                                                                                                                             |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------|
| PocketBase             | <img src="./assets/Pocket.png" width="35">                                                                                                         |


 

  
