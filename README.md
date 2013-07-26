# always-tail

Node.js module for continuously tailing a file.

It differs from other `tail` modules in that it survives truncates, 
file rollovers (e.g. `mv /var/log/test /var/log/test.1`), and unlink.

It does this by monitoring the filename, and when the inode changes, 
it will continue to read to the end of the existing file descriptor.
It emits a 'line' event when a new line is read. 

## Installation

npm install always-tail

## Example

```js
var Tail = require('always-tail');
var fs = require('fs');
var filename = "/tmp/testlog";

if (!fs.existsSync()) fs.writeFileSync(filename, "");

var t = new Tail(filename, '\n');

tail.on('line', function(data) {
  console.log("got line:", data);
});


tail.on('error', function(data) {
  console.log("error:", data);
});

tail.watch();
```

## Credits

Code is heavily modified from the node-tail module (https://github.com/forward/node-tail)

## License

MIT 
