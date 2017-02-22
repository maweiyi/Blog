##### Readable
```
var Stream = require('stream');

var source = ['a', 'b', 'c'];
var readable = Stream.Readable({
    read: function () {
        var data = source.shift() || null;
        console.log('push', data);
        this.push(data)
    }
});

readable.on('end', function () {
    console.log('end')
});

readable.on('data', function (data) {
    console.log('data', data)
});


```

##### Writeable
```
var Stream = require('stream');

var writable = Stream.Writable();

writable._write = function (data, _, next) {
    console.log(data);
    next();
};

writable.write('a');
writable.write('b');
writable.end();

```