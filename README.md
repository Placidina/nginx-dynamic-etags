# Name

`nginx-dynamic-etags` - Nginx C module to handling ETag / If-None-Match on proxied content.

* [Status](#status)
* [Synopsis](#synopsis)
* [Installation](#installation)
* [About](#about)

## Status

This module is production ready.

## Synopsis

```sh
http {
    map $request_uri $etag {
        default "off";

        /api/foo "on";
        /api/bar "on";
    }

    server {
        listen 80;

        location ~ ^/api/.* {
            dynamic_etags $etag;

            proxy_http_version 1.1;
            proxy_set_header Connection "";

            proxy_pass http://127.0.0.1:8080;
        }
    }
}
```

## Installation

1. Grab the nginx source code from [nginx.org](http://nginx.org/).
2. and finally build the source with this module:

```sh
./configure ... \
    --add-module=/path/to/nginx-dynamic-etags

make -j2
make install
```

## About

This module meets the needs of the [`kali/nginx-dynamic-etags`](https://github.com/kali/nginx-dynamic-etags) module, to implements `nginx map` to enable `etag`.
