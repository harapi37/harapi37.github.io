## How to Use the APIs/ Databases:

The following text will describe, with code samples in JavaScript, how to "import" and use "random" or "specific" entries in the JSON files.
It will be a fairly simple, for everyone to understand, this is just one of many ways and there might be way shorter answers out there.

First import the library:

```
https = require('https')
```

Then, to get the data in a JSON object, we write the function httpGet():

```
function httpGet() {
  return new Promise(((resolve, reject) => {
    var options = {
        host: 'harapi37.github.io',
        port: 443,
        path: '/apis/jr_api.json',
        method: 'GET',
    };
    
    const request = https.request(options, (response) => {
    //   response.setEncoding('utf8');
      let returnData = '';

      response.on('data', (chunk) => {
        returnData += chunk;
      });

      response.on('end', () => {
        resolve(JSON.parse(returnData));
      });

      response.on('error', (error) => {
        reject(error);
      });
    });
    request.end();
  }));
}
```

Since these are more of databases without functions, you'll need to retrieve the specific entry or a random entry yourself:

To get a _random_ entry you need to implement... 

(1) ... either write the function with min (inclusive) and max (inclusive):

```
function getRandomInt(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
```

(2) ... or write the function with min (inclusive) and max (exclusive):

```
function getRandomArbitrary(min, max) {
     return Math.random() * (max - min) + min;
}
```

(3) And then call it with max as response.all (bc the number of entries in the JSON object is stored in the object "all"):

```
const response = await httpGet();
var rand = getRandomInt(1, response.all)
var quote = response.quotes[rand]
```

And to get a _specific_ entry just simply go for a number that you choose:
```
const response = await httpGet();
var num = 6
var quote = response.quotes[num]
```
