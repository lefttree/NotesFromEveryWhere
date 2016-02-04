# Web Cache

## What

A Web cache sits between one or more Web servers (also known as origin servers)
and a client or many clients, and watches requests come by, saving copies of
the responses — like HTML pages, images and files (collectively known as
representations) — for itself.

2 reasons that web caches are used:

- reduce latency
    + It takes less time for the client to get the representation and display it
- reduce network traffic
    + reduces the bandwidth used by a client

## Kinds of Web Caches

### Browser Caches

Set aside a section of your computer's **hard disk** to stro representations. It
will check to make sure that the representations are fresh, usually once a session.

It's especially useful when users hid the **back** button or click a link to see
a page they've just looked at.

### Proxy Caches

Web proxy caches work on the same principle, but a much larger scale. Proxies
serve hundreds or thousands of users in the same way. Large corporations and ISPs
often set them up on standablone devices.

Requests have to be routed to them. it's a type of *shared cache*.

### Gateway Caches

Also known as "reverse proxy caches" or "surrogate caches". It's typically deployed
by Webmasters themselves. Requests can be routed to gateway caches by a number of
methods, but typically some form of **load balancer** is used.

**CDN** distributes gateway caches throughout the network.


## How Web Caches Work

Some rules are set in the protocol, and some are set by the administrator of
the cache.

Common rules

1. If the response’s headers tell the cache not to keep it, it won’t.
2. If the request is authenticated or secure (i.e., HTTPS), it won’t be cached by shared caches.
3. A cached representation is considered fresh (that is, able to be sent to a client without checking with the origin server) if:
    - It has an expiry time or other age-controlling header set, and is still within the fresh period, or
    - If the cache has seen the representation recently, and it was modified relatively long ago.
   Fresh representations are served directly from the cache, without checking with the origin server.
4. If a representation is stale, the origin server will be asked to validate it, or tell the cache whether the copy that it has is still good.
5. Under certain circumstances — for example, when it’s disconnected from a network — a cache can serve stale responses without checking with the origin server.

If no validator (an ETag or Last-Modified header) is present on a response, and
it doesn't have any explicit freshness information, it will usually — but not
always — be considered `uncacheable`.

`freshness` and `validation` are the most important ways that a cache works with
content.

## How to control caches

### HTML Meta Tags and HTTP Headers

`meta tags` are often used in the belief that they can make a doc as uncacheable,
or expires it at a certain time.

They are not very effective, because they're only honored by a fre browser caches,
not proxy caches(which almost never read the HTML).

Typical HTTP 1.1 response headers might look like this:

```
HTTP/1.1 200 OK
Date: Fri, 30 Oct 1998 13:19:41 GMT
Server: Apache/1.3.3 (Unix)
Cache-Control: max-age=3600, must-revalidate
Expires: Fri, 30 Oct 1998 14:19:41 GMT
Last-Modified: Mon, 29 Jun 1998 02:28:12 GMT
ETag: "3e86-410-3596fbbc"
Content-Length: 1040
Content-Type: text/html
```

### Pragma HTTP Headers

`pragma: no-cache` only works with a few caches.

### `Expires` HTTP Header

it tells all caches how long the associated representation is fresh for. After 
that time, caches will always check back with the origin server.

`Expires` headers are supported by practically every cache.

The only value valid in an Expires header is a HTTP date. It's a GMT time.

Limitations:

- the clocks on the web server and the cache must be synchronized.
- it's easy to forget, if you don't update before it passes, each and every request
will go back to the origin server.

### Cache-Control HTTP Headers

- `max-age=[seconds]`
- `s-maxage=[seconds]`
- `public`
- `private`
- `no-cache`
- `no-store`
- `must-revalidate`
- `proxy-revalidate`

Example: `Cache-Control: max-age=3600, must-revalidate`

## Validator and Validation

Validation is used by servers and caches to communicate when a representation has
changed. By using it, caches avoid having to download the entire representation
when they already have a copy locally, but not sure if it's fresh.

Validator:

1. `Last-Modified`
    most popular
2. `ETag`

Most modern web servers will generate both `ETag` and `Last-Modified` headers to
use as validators for static content automatically. However, they don't know
enough about dynamic content(like CGI, ASP or database sites).

## Tips for building a Cache-Aware Site

- Uses URL consistently
- Use a common library of images
- make caches store images and pages that don't change often by using a 
`Cache-Control: max-age` header with a large value
- make caches recognise regularly updated pages
- if a resource changes, change its name
- Don't change files unnecessarily
- Use cookies only where necessary
- Minimize use of SSL
- check pages with [REDbot](https://redbot.org/)

## Writing Cache-Aware Scripts

If the content of the script changes only depending on what’s in the URL, it is
cacheable;

if the output depends on a cookie, authentication information or other external
criteria, it probably isn’t.

- The best way to make a script cache-friendly(as well as perform better) is to
dump its content to a plain file whenever it changes.
- another way is to set an age-related header for as far in the future as practical.
- make the script generate a validator.

## FAQ

1. need to keep statistics on how many people visit my page

Select **ONE** small item on a page and make it uncacheable.

2. my pages are password-protected, how do proxy caches deal with them?

Be default they are considered private. Make it cacheable but still authenticated 
for every use, combine

`Cache-Control: public, no-cache`

3. images expire a month from now, but need to update them

Change any links to them. it's best to make static images and other things very
cacheable, while keeping the HTML pages that refer to hem on a tight leash.

## Systems

### Forward

### Reverse


## References

- [Caching Tutorial](https://www.mnot.net/cache_docs/)
- [Web caching basics](https://www.digitalocean.com/community/tutorials/web-caching-basics-terminology-http-headers-and-caching-strategies)
