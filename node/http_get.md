Get
===

```javascript
var http = require('http');
var jschardet = require('jschardet');
var iconv = require('iconv-lite');

var options = {
	hostname: "www.sina.com.cn"
};

http.request(options, function (res) {
	var buffers = [];
	var buf, encoding, body;
	res.on('data', function (chunk) {
		buffers.push(chunk);
	});

	res.on('end', function () {
		buf = Buffer.concat(buffers);
		console.log(jschardet.detect(buf));
		encoding = jschardet.detect(buf).encoding;
		body = iconv.decode(buf, encoding);
		console.log(body);
	});
}).end();
```