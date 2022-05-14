```js
function promisify(f) {
    return function() {
        var args = Array.prototype.slice.call(arguments);

        return new Promise(function(resolve, reject) {
            args.push(function(err, data) {
                if (err) reject(err);
                else resolve(data);
            });
            f.apply(null, args);
        });        
    }

}
```

