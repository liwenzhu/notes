POST
====

```javascript
'use strict';

var http = require('http');
var querystring = require('querystring');

var postData = querystring.stringify({
    userName: 'vincent'
    , password: 'liwenzhu'
    , email: 'abc@test.com'
});

var options = {
    hostname: 'et.vm.com'
    , port: 3000
    , path: '/api/register'
    , method: 'POST'
    , headers: {
	'Content-Type': 'application/x-www-form-urlencoded',
	'Content-Length': postData.length
    }
};

var req = http.request(options, function(res) {
    console.log('STATUS: ' + res.statusCode);
    console.log('HEADERS: ' + JSON.stringify(res.headers));
    res.setEncoding('utf8');
    res.on('data', function (chunk) {
	console.log('BODY: ' + chunk);
    });
});

req.on('error', function(e) {
    console.log('problem with request: ' + e.message);
});

// write data to request body
req.write(postData);
req.end();

```