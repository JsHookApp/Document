# http

Used for network requests. Note that the hooked application needs to have network access permissions

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

//or

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

The key and value in the headers must both be string types. When data is an object, it is a form submission. The header will add content-type:application/x-www-form-urlencoded. If content-type:application/json is submitted, it is necessary to make sure that the data parameter type is string
