---
comments: true
layout: post
title : popular nodejs modules
categories : 
- Stack
tags : 
- NodeJS
---



just for memory


- **colors** [https://github.com/marak/colors.js/]()

```javascript
var colors = require('./colors');
console.log('hello'.green); // outputs green text
console.log('i like cake and pies'.underline.red) // outputs red underlined text
console.log('inverse the color'.inverse); // inverses the color
console.log('OMG Rainbows!'.rainbow); // rainbow (ignores spaces)
```
	
- **mkdirp** [https://github.com/substack/node-mkdirp]()

```javascript
var mkdirp = require('mkdirp');
mkdirp('/tmp/foo/bar/baz', function (err) {
if (err) console.error(err)
    else console.log('pow!')
});
```
- ** iconv-lite ** [https://github.com/ashtuchkin/iconv-lite]()

```javascript
var iconv = require('iconv-lite');

// Convert from an encoded buffer to string.
str = iconv.decode(buf, 'win1251');

// Convert from string to an encoded buffer.
buf = iconv.encode("Sample input string", 'win1251');
```
- ** send ** [https://github.com/visionmedia/send]()

```javascript
var http = require('http');
var send = require('send');
var url = require('url');

var app = http.createServer(function(req, res){
  // your custom error-handling logic:
  function error(err) {
    res.statusCode = err.status || 500;
    res.end(err.message);
  }

  // your custom directory handling logic:
  function redirect() {
    res.statusCode = 301;
    res.setHeader('Location', req.url + '/');
    res.end('Redirecting to ' + req.url + '/');
  }

  // transfer arbitrary files from within
  // /www/example.com/public/*
  send(req, url.parse(req.url).pathname)
  .root('/www/example.com/public')
  .on('error', error)
  .on('directory', redirect)
  .pipe(res);
}).listen(3000);
```
- ** connect ** [https://github.com/senchalabs/connect]()

```javascript
var connect = require('connect')
  , http = require('http');

var app = connect()
  .use(connect.favicon())
  .use(connect.logger('dev'))
  .use(connect.static('public'))
  .use(connect.directory('public'))
  .use(connect.cookieParser())
  .use(connect.session({ secret: 'my secret here' }))
  .use(function(req, res){
    res.end('Hello from Connect!\n');
  });

http.createServer(app).listen(3000);
```
---
伊泽  
2013-5-20于杭州