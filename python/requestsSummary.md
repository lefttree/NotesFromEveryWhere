# requests

## HTTP Requests

```python
r = requests.get('https://api.github.com/events')
r = requests.post("http://httpbin.org/post", data = {"key":"value"})
r = requests.put("http://httpbin.org/put", data = {"key":"value"})
r = requests.delete("http://httpbin.org/delete")
r = requests.head("http://httpbin.org/get")
r = requests.options("http://httpbin.org/get")
```

`r` is a [Response](http://docs.python-requests.org/en/latest/api/#requests.Response) object

## parameters in URLs

**params**

```python
>>> payload = {'key1': 'value1', 'key2': 'value2'}
>>> r = requests.get("http://httpbin.org/get", params=payload)
```

values that are `None` will not be sent

## Response 

- `r.url`
- `r.text` 
    + requests will auto decode content from the server
- `r.encoding`
- `r.content`
    + see the response body as bytes
- `r.json()`
    + would raises an exception if JSON decoding fails
- `r.status_code`
- `r.headers`
- `r.raw`
    + raw socket, make sure to set `stream=True`

```python
>>> r = requests.get('https://api.github.com/events', stream=True)
>>> r.raw
<requests.packages.urllib3.response.HTTPResponse object at 0x101194810>
>>> r.raw.read(10)
'\x1f\x8b\x08\x00\x00\x00\x00\x00\x00\x03'
```

In general, however, you should use a pattern like this to save what is being streamed to a file:

```python
with open(filename, 'wb') as fd:
    for chunk in r.iter_content(chunk_size):
        fd.write(chunk)
```

## Custom Headers

**headers**

```python
headers = {'user-agent': 'my-app/0.0.1'}
r = requests.get(url, headers=headers)
```

## POST requests

**data**

Send form-encoded data like an HTML form

```python
>>> payload = {'key1': 'value1', 'key2': 'value2'}
>>> r = requests.post("http://httpbin.org/post", data=payload)
```

If you pass in a string instead of a dict, that data will be posted directly.

```python
>>> import json
>>> payload = {'some': 'data'}

>>> r = requests.post(url, data=json.dumps(payload))
```

## POST a Multipart-Encoded File

**files**

```python
>>> files = {'file': open('report.xls', 'rb')}

>>> r = requests.post(url, files=files)
```

## Cookies

```python
>>> r = requests.get(url)

>>> r.cookies['example_cookie_name']
```

To send your own cookies **cookies**

```python
>>> cookies = dict(cookies_are='working')

>>> r = requests.get(url, cookies=cookies)
>>> r.text
```

## Timeouts

`requests.get('http://github.com', timeout=0.001)`

## Session Objects

The session object allows you to persist certain parameters across requests. It also persists cookies across all requests made frome the Session instance, and use urllib3's connection pooling.

### persist some cookies across requests

```python
s = requests.Session()

s.get('http://httpbin.org/cookies/set/sessioncookie/123456789')
r = s.get("http://httpbin.org/cookies")
```

### provide default data

```python
s = requests.Session()
s.auth = ('user', 'pass')
s.headers.update({'x-test': 'true'})

# both 'x-test' and 'x-test2' are sent
s.get('http://httpbin.org/headers', headers={'x-test2': 'true'})
```

method-level parameters override session parameters, but they are not persisted across requests.

To manually add cookies, use cookies utiluity functions

- `dict_from_cookiejar(cj)`
- `cookiejar_from_dict(cookie_dic, cookiejar=None, overwrite=True)`
- `add_dict_to_cookiejar(cj, cookie_dict)`
- `RequestsCookieJar(policy=None)`

