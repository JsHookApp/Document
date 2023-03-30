# http

用于进行网络请求，注意，需要被hook的应用拥有网络访问权限

## http.get(url,headers,function)

`参数`:

`url`: string

`headers`: object

`function`: function

示例：

```js
http.get('https://www.baidu.com', {
    'test': 1
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

`参数`:

`url`: string

`data`: object

`headers`: object

`function`: function

示例：

```js
http.post('https://www.baidu.com', {
    'user': 'me'
}, {
    'test': 1
}, {
    success: function (result) {
        console.log(result);
    },
    error: function (err) {
        console.log(err);
    }
});
