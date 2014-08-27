Restart dead child cluster
===========================

Demo for stable cluster code. this is a master-slave model.

Master
======

```javascritp
'use strict';

var cluster = require('cluster');
var numCPUs = require('os').cpus().length;

cluster.setupMaster({
	exec: "worker.js"
});

for (var i = 0; i < numCPUs; i++) {
	createWorker();
}

function createWorker () {
	var worker = cluster.fork();
	worker.on('message', function (msg) {
		// DO LOGIC HERE...
	});
};

cluster.on('online', function (worker) {
	console.log('worker %s is ready.', worker.id);
});

cluster.on('exit', function (worker, code, signal) {
	console.log('worker %d died (%s). restarting...',
	worker.process.pid, signal || code);
	createWorker();
});
```

Slave
======

```javascript
process.on('message', function(msg) {
	//DO YOUR LOGIC HERE
});

process.send({}); // send data to master.
```