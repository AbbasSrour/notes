### HTTP Methods
* **Get:** Read Data
* **Post:** Insert Data
* **Put:** Update Data
* **Delete:** Delete Data

### Headers
To specify the headers of the response message, we use the  `writeHead()` method for the `HTTP Module` .
```js
const server = http.createServer((req,res)=>{
res.writeHead(<response-code>, {'content-type': '...'});
});
```