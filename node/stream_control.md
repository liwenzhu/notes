控制流对象的流量
==============

可以实现类似迅雷的下载速度控制之类的需求。

```javascript
req = http.request(options, function (res) {
		buffers = [];
		var startTime = new Date();
		var tmpSentBytes = 0, elapsedTime, assumedTime, lag;
		res.on('data', function (chunk) {
			if(!buffers)
				return process.send({});
			buffers.push(chunk);
			tmpSentBytes += chunk.length;
			elapsedTime = new Date() - startTime;
	        assumedTime = tmpSentBytes >> SPEED_LIMIT;
	        lag = assumedTime - elapsedTime;
		    if (lag > 0) {
		      // console.log('too fast, download will resume in: ' + lag + 'ms');
		      res.pause();
		      setTimeout(function () {
		        res.resume();
		      }, lag);
		    }
		});
	});
req.end();
```

基本的思路就是计算数据的所用的时间与设定的下载速度进行对比，如果速度过快就通过
pause和resume这两个函数进行调节。
