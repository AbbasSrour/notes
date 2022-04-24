### Def
Streams are used to read or write sequentially from continuous or big files in chunks, 
streams extend event emitter class and can be used on event methods.

NodeJS there are four types of streams:
1. Writable: Used to write data sequentially 
2. Readable: Read data sequentially
3. Duplex: Read and write data sequentially
4. Transform: Data can be modified while reading and writing

### Usage
```js
const { createReadStream } = require('fs');
const stream = createReadStream('path-to-file', { options });
stream.on('data', (result)=>{
// do some shit
});
```

### Options
* **highWaterMark:** control the size of the buffer
