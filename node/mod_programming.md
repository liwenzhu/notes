Mod
===

```javascript
var count = 5000000000;
var c;

console.time("% compute");
for (var i = 0; i < count; i++) {
	c = i % 32;
}
console.timeEnd("% compute");

console.time("& compute");
for (var i = 0; i < count; i++) {
	c = i & 31;
}
console.timeEnd("& compute");
```

output:

```
% compute: 37706ms
& compute: 8556ms
[Finished in 46.4s]
```