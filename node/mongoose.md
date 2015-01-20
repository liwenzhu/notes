Mongoose
========

Mongoose connect two database


```javascript

var mongoose = require('mongoose');
var Schema = mongoose.Schema;
var schema1 = new Schema({ name: String });
var schema2 = new Schema({ num: Number});
var conn1 = mongoose.createConnection("mongodb://localhost/server");
var conn2 = mongoose.createConnection("mongodb://localhost/resource");
var model1 = conn1.model('model1',schema1);
var model2 = conn2.model('model2',schema2);

```
