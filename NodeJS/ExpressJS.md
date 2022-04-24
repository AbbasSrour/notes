Express is a framework for [[Events]] that simplifies the process of creating a nodejs server.
```js
const express = require('express');
const app = express()

app.listen(<port>, ()=>{
// on server creating callback
})
```

### Methods
Express has builtin methods that handle [[Events#HTTP Methods|HTTP Methods]]   
#### get
```js
app.get('requseted-file',(req, res)=>{
	res.send();
});
```
#### all
This will specify 
