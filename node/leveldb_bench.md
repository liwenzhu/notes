Benchmark of leveldown
======================

```javascript
/**
 * Module dependencies.
 */

var uubench = require('uubench');

fs = require('fs');
var leveldown = require('leveldown');
db = new leveldown('/tmp');

db.open(function(){
  db.put('bench', 'bench', function(){
    suite = new uubench.Suite({
      start: function(){
        console.log();
      },

      result: function(name, stats){
        var persec = 1000 / stats.elapsed
          , ops = stats.iterations * persec;
        console.log('  \033[90m%s : \033[36m%s \033[90mops/s\033[0m', name, ops | 0);
      },
      
      done: function(){
        console.log();
      }
    });
    
    suite.bench('read benchmark', function(next){
      db.get('bench', function(){
        next();
      })
    });

    suite.bench('write benchmark', function(next){
      db.put(new Date(), 'aaa', function(){
        next();
      });
    });

    suite.run();
  });

});


```