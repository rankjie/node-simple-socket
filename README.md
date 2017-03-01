# node-simple-socket

Wrapper for [Node.js sockets](https://nodejs.org/api/net.html#net_class_net_socket) that makes it easy to send data compressed and crypted ([RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) / [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)).

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MMUUNRQ8ZUJEN) [![](https://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?fid=o62pkd&url=https%3A%2F%2Fgithub.com%2Fmkloubert%2Fnode-simple-socket)

## Install

```bash
npm install simple-socket --save
```

## Usage

### Import

```javascript
var simpleSocket = require('simple-socket');
```

The [TypeScript](https://www.typescriptlang.org/) way:

```typescript
import * as simpleSocket from 'simple-socket';
```

### Create a server

```javascript
// listening for new connection
// on port 5979
var server = simpleSocket.listen(5979, function(err, newConnection) {
    // callback for new connections

    if (err) {
        // an error occurred while creating
        // the client connection
    }
    else {
        // work with new connection
    }
}).then(function(server) {
    // the server is now listening
}, function(err) {
    // could not listening on port
});
```

### Connect to a server

```javascript
// listening for new connection
// on port 5979
var server = simpleSocket.connect(5979, 'server.example.com').then(function(socket) {
    // connection established
}, function(err) {
    // could not connect
});
```

### Send and receive data

#### Raw data

Send:

```javascript
var dataToSend = new Buffer('Hello, TM!', 'utf8');

senderSocket.write(dataToSend).then(function(sendData) {
    // data has been send
}, function(err) {
    // could not send data
});
```

Receive:

```javascript
recipientSocket.read().then(function(receivedData) {
    // data has been arrived
}, function(err) {
    // could not receive data
});
```

#### Strings

Send:

```javascript
senderSocket.write('Hello, MK!').then(function(sendData) {
    // string has been send
}, function(err) {
    // could not send string
});
```

Receive:

```javascript
recipientSocket.readString().then(function(str) {
    // str === "Hello, MK!"
}, function(err) {
    // could not receive string
});
```

#### JSON objects

Send:

```javascript
var myObject = {
    TM: 5979,
    MK: '23979',
    PZSUX: true
};

senderSocket.writeJSON(myObject).then(function(sendData) {
    // data has been send
}, (err) => {
    // could not send data
});
```

Receive:

```javascript
recipientSocket.readJSON().then(function(obj) {
    // obj.TM === 5979
    // obj.MK === '23979'
    // obj.PZSUX === true
}, function(err) {
    // could not receive obj
});
```
