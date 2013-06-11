---
layout: index
---
Stardog.js
==========

Licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0)  
_Current Version **0.0.5**_ 

Stardog.js JavaScript Framework for Node.js to develop apps with the [Stardog RDF Database](http://stardog.com).  

![Stardog](http://stardog.com/_/img/sdog.png)   

For detailed documentation, see the [annotated source](http://clarkparsia.github.io/stardog.js/docs/stardog.html).

## What is it? ##

This framework wraps all the functionality of a client for the Stardog DBMS, and provides access to a full set of functions such as executing SPARQL Queries, administration tasks on Stardog, and the use of the Reasoning API.

All the implementation uses the HTTP protocol, since most of Stardog functionality is available using this protocol. For more information, go to the Stardog's [Network Programming](http://stardog.com/docs/network/) documentation.

The framework is currently targeted to Node.js (the latest version) and it has not been fully tested in the browser, but future versions will be have browser compatibility.
You'll also need [npm](https://npmjs.org) to run the test cases and install the dependencies.

## Installation

To install stardog.js locally from the npm registry simply execute:

    npm install stardog
    
That will fetch the latest version of stardog.js in the npm registry, [more details](https://npmjs.org/package/stardog).

## Development ##

To get started, just clone the project. You'll need a local copy of Stardog to be able to run the tests. For more information on starting the Stardog DB service and how it works, go to [Stardog's documentation](http://stardog.com/docs/), where you'll find everything you need to get up and running with Stardog.

Go to [http://stardog.com](http://stardog.com), download and install the database and load the data provided in `data/` using the script in the repository. Start Stardog with the `http` port on `5823` with the following command:

  $ stardog-admin server start --http 5823

Once you have Stardog running, execute the following command:

    $ npm install
    $ bower install

This will install all the dependencies using npm (for node) and bower (for browser), once this is done, run the test cases.

All tests should pass.

### Running Tests

Run all the test cases in `test/spec`. Having the Stardog server running, execute the following commands:

1\. Load the test data using the provided script:

    $ ./load_test_data.sh

2\. Start the proxy via:

    $ node test/testCORS.js

3.\ Run the test suite:

#### In the Browser

    open test/index.html

#### In node.js

    $ npm test    


## Version details ##

Stardog.js depends of the Stardog HTTP API, and any change in this API will be supported by Stardog.js. Here's a list of version compatibility between __Stardog__ and  __Stardog.js__:

| Stardog Version | Stardog.js Version |
| --------------- | ------------------ |
| <= 1.1.5        | <= 0.0.3           |
| 1.2             | >= 0.0.4           |


## Quick Example ##

### Node.js

    var stardog = require("stardog");
     
    var conn = new stardog.Connection();
     
    conn.setEndpoint("http://myserver:myport/");
    conn.setCredentials("username", "password");
     
    conn.query({ 
            database: "myDB", 
            query: "select distinct ?s where { ?s ?p ?o }",  
            limit: 10, 
            offset: 0 
        },
        function (data) {
            console.log(data.results.bindings);
    });
    
### Browser

__NOTE__: the Endpoint is a proxy to the Stardog HTTP interface in order to avoid CORS issues (an example can be fount in `test/testCORS.js`.

    <script src="js/stardog.js" type="text/javascript"></script>
    …
    <script type="text/javascript">
        var conn = new Stardog.Connection();
        conn.setEndpoint("/stardog");
        conn.setReasoning("QL");
        conn.setCredentials("browser", "secret");
    </script>

## NOTE ##

This framework is in continuous development, please check the [issues](https://github.com/clarkparsia/stardog.js/issues) page. You're welcome to contribute.