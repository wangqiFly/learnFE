```javascript


function promiseControl(max, array) {
    var maxCount = max;
    var count = 0;
    var ayscArray = array;

    let process = function (promise) {

        if (promise == null) {
            return;
        }

        if (count >= maxCount) {
            ayscArray.push(promise);
        } else {
            count++;
            promise.then(() => {
                count--;
                process(ayscArray.shift());
            })
        }
    }

    return process;
}

let myPromise = promiseControl(3, []);


for (i = 0; i < 1000; i++) {
    let t = i;
    myPromise(new Promise(function (resolve, reject) {

        setTimeout(() => {
            console.log(t);
            resolve(t);
        }, 1000)

    }));
}
```

