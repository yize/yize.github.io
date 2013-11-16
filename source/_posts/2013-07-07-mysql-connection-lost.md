---
comments: true
layout: post
title :  node.js Connection lost The server closed the connection.
categories : 
- Stack
tags : 
- Mysql
- NodeJS
---


### mysql模块

今天访问了下内网的一台服务器，发现挂掉了，SSH上去看了下`nohup.out`,发现报错了
```haskell
    events.js:71
            throw arguments[1]; // Unhandled 'error' event
                           ^
    Error: Connection lost: The server closed the connection.
        at Protocol.end (/var/www/html/utci/node_modules/mysql/lib/protocol/Protocol.js:73:13)
        at Socket.onend (stream.js:66:10)
        at Socket.EventEmitter.emit (events.js:126:20)
        at TCP.onread (net.js:417:51)
```

这个错误的大概意思就是，未处理的`error`事件

原因是：mysql的连接久了以后，超时了。

解决方法是：

增加`error`事件的监听

database.js:

```javascript
    var mysql = require('mysql'),
        settings = require('../settings');

    module.exports.getConnection = function () {
        if ((module.exports.connection) && (module.exports.connection._socket)
            && (module.exports.connection._socket.readable)
            && (module.exports.connection._socket.writable)) {
            return module.exports.connection;
        }
        console.log(((module.exports.connection) ?
            "UNHEALTHY SQL CONNECTION; RE" : "") + "CONNECTING TO SQL.");
        var connection = mysql.createConnection({
            host: settings.host,
            port: settings.port,
            database: settings.db_name,
            user: settings.username,
            password: settings.password,
            //中文读取
            charset: "utf8"
        });
        connection.connect(function (err) {
            if (err) {
                console.log("SQL CONNECT ERROR: " + err);
            } else {
                console.log("SQL CONNECT SUCCESSFUL.");
            }
        });
        connection.on("close", function (err) {
            console.log("SQL CONNECTION CLOSED.");
        });
        connection.on("error", function (err) {
            console.log("SQL CONNECTION ERROR: " + err);
        });
        module.exports.connection = connection;
        return module.exports.connection;
    };

    // Open a connection automatically at app startup.
    module.exports.getConnection();
    // If you've saved this file as database.js, then get and use the
    // connection as in the following example:
    // var database = require(__dirname + "/database");
    // var connection = database.getConnection();
    // connection.query(query, function(err, results) { ....
```
---
伊泽  
2013-07-07于杭州