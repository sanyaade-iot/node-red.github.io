---
layout: default
title: Embedding into an existing app
---   

*This is new and subject to tweeking as we play with it more*

It is possible to embed Node-RED into a larger application. A typical scenario
would be where you use Node-RED to generate flows of data that you want to
display on a web dashboard - all from the same application.


Add `node-red` to the module dependencies in your application's `package.json`,
along with any of the individual node dependencies you may have.

The following is a minimal example of embedded the runtime into a wider Express
application.

    var http = require('http');
    var express = require("express");
    var RED = require("node-red");
    
    var app = express();
    app.use("/",express.static("public"));
    
    var server = http.createServer(app);
    
    var settings = {};
    
    // initialise the runtime with a server
    // and settings
    RED.init(server,settings);
    
    // serve the editor UI from /red
    app.use("/red",RED.app);

    server.listen(8000);
    
    // Start the runtime
    RED.start();

When this approach is used, the `settings.js` file included with Node-RED is not
used. Instead, the settings are passed to the `RED.init` call as shown above.

Furthermore, the following settings are ignored as they are left to you to
configure the Express instance as you want it:

 - `uiPort`
 - `httpAuth`
 - `httpRoot`
 - `https`

