# tri-state
A status manager

```js
var exec = require('child_process').exec;

// ...
// 假設 gpio 已經 export 出來, direction 也設定好了
// 以下程式碼沒有測試過, 寫個大概
// 它在 /app/model/model.js 裡面第 24 行附近

so3.init('lightCtrl', 0, {
    onOff: {
        read: function (cb) {
            exec('cat /sys/class/gpio/gpioXX/value', function (err, stdout, stderr) {
                if (err) {
                    cb(err);
                } else {
                    // stdout is result, I think its a string '0' or '1',
                    // we can use parseInt() to make it a number. 這個請自己確定一下囉
                    cb(null, parseInt(stdout);  
                }
            });
        },
        write: function (val, cb) {
            var valWritten = val ? 1 : 0;
            exec('echo ' + valWritten + ' > /sys/class/gpio/gpioXX/value', function (err, stdout, stderr) {
                if (err)
                    cb(err);
                else
                    cb(null, val);
            });
        }
    }
});
```
