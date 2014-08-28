REGEXP
======

Extract body content from html page.

```javascript
var bodyContent = /<body.*?>([\s\S]*)<\/body>/.exec(htmlCode);
```