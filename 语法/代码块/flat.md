```js
let arr = [1, [3, 2]]


function f(arr) {
    if (Array.isArray(arr)) {
        return arr.reduce((prev, item) => {
            return Array.isArray(item) ? prev.concat(f(item)) : prev.concat(item)
        }, [])
    } else {
        throw new Error("arr + ' is not array'")
    }
}

console.log(arr);

console.log(f(arr));

```

