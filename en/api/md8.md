# http

HTTP requests. Note: the hooked app must have network access permission.

## http.get(url,headers,function)

`Parameters`:

`url`: string

`headers`: object

`function`: function

Example:

```javascript
http.get('http://xxxxx.com', {
    'test': '1'
}, {
    success: function (result) {
        console.log(result);
    },
    error: function (err) {
        console.log(err);
    }
});
```

## http.post(url,data,headers,function)

`Parameters`:

`url`: string

`data`: object

`headers`: object

`function`: function

Example:

```javascript
http.post('http://xxxxx.com', {
    'user': 'me'
}, {
    'test': '1'
}, {
    success: function (result) {
        console.log(result);
    },
    error: function (err) {
        console.log(err);
    }
});

// Or with JSON body

http.post('http://xxxxx.com', JSON.stringify({
    'user': 'me'
}), {
    'content-type': 'application/json'
}, {
    success: function (result) {
        console.log(result);
    },
    error: function (err) {
        console.log(err);
    }
});
```

## Notes

Header keys and values must both be string type. When data is an object, it's submitted as form data with `content-type: application/x-www-form-urlencoded`. For `content-type: application/json`, ensure the data parameter is a string.
