# JSONP

## JSONP Request

Because of *same origin policy*, regula XHR get will get a HTTP error.

JSONP makes use of the ability of `script` tags to fetch content from any server.

JSONP requests are not dispatched using the XMLHTTPRequest, instead a `<script>`
tag is created, whose source is set the the target URL. Then this script tag is
added to the DOM.

```javascript
var logIt = function(data) {
    console.log(data[0].text);
}

var tag = document.createElement("script");
tag.src = 'somewhere_else.php?callback=logIt;' // extra parameter callback=logIt

document.getElementsByTagName("HEAD")[0].appendChild(tag);
```

## Concern

safety. suggests that should valid the response as pure JSON.

`JSON.stringify` then `JSON.parse` might help
