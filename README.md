# ELWIS
Elm/Elchemy Language Web Interface for Server

**ELWIS** is a dead simple abstraction of HTTP for Elm.

## Summary

The ELWIS specification consists of headers, requests, responses, apps, and middleware.  Below are examples of each.

**ELWIS requests**.
    
    {server_port = "80",
     server_name = "127.0.0.1",
     remote_addr = "127.0.0.1",
     uri = "/",
     scheme = "http",
     query_string = "",
     method= "get",
     content_type = "",
     content_length = 0,
     character_encoding = "",
     body = "",
     headers:
       \[accept_charset "ISO-8859-1,utf-8;q=0.7,*;q=0.3",
        connection "keep-alive",
        host "localhost:8000",
        \]
     }

**ELWIS responses**.

    {status: 200,
     headers = [content_type "text/plain"],
     body: "Hello!"}

**ELWIS apps**.

    app req = 
        if req.uri == "/favicon.ico" then
            {status = 404, headers = [], body = "Not Found"}
        else
            { status = 200
            , headers = [content_type "text/html"]
            , body = "<h1>Hello!</h1>"
            }
            
**ELWIS middleware**.
    
    wrap_as_upcase app req = 
        let resp = app req
        in
        { status: resp.status
        , headers = resp.headers
        , body = String.toUpper resp.body -- just demonstrating the use with silly case
        }

For the detailed specification, see [`SPEC.md`](http://github.com/elm-elwis/elwis/spec.md).

## Getting started

### Installation

To install, type

    $ pip install pump

or grab the code from [Github](https://github.com/adeel/pump):

    $ git clone git://github.com/adeel/pump.git
    $ cd pump
    $ python setup.py install

### Running your app

Pump comes with an adapter for the [Paste WSGI server](http://pythonpaste.org/modules/httpserver.html).  If you don't have that installed, do

    $ pip install Paste

and then to run your app:

    import pump
    pump.adapters.serve_with_paste(app, {"port": 3000})

Soon, Pump will come with adapters for other popular WSGI servers.

## Thanks

ELWIS was heavily inspired by Python's [Pump](https://github.com/adeel/pump).  Thanks, Adeel Khan!

## License

Copyright (c) 2019 Pavan Mishra <reachme@pavanmishra.com>.

MIT license.
