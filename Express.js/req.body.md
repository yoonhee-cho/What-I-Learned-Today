# req.body

- generally used in POST/ PUT requests
- use it when you want to send JSON data to the server

## How to send data in request body
```
axios.post('/giraffe', {
    key1: 'value1',
    key2: 'value2'

})
.then(response => {
    ...
})
.catch(error => {
    ...
})

How to get data from request body

app.get('/giraffe', (req,res) => {
    console.log(req.body.key1) //value1
    console.log(req.body.key2) //value2
})
```

- post/put method로 보내는 obj가 req.body

```
var express = require('express'); 
var app = express();  
var PORT = 3000; 
  
// For parsing application/json 
app.use(express.json()); 
  
// For parsing application/x-www-form-urlencoded 
app.use(express.urlencoded({ extended: true })); 
  
app.post('/profile', function (req, res) { 
  console.log(req.body); 
  res.send(); 
}); 
  
app.listen(PORT, function(err){ 
    if (err) console.log(err); 
    console.log("Server listening on PORT", PORT); 
}); 
```