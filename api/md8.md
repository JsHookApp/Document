# http

用于进行网络请求，注意，需要被hook的应用拥有网络访问权限

## http.get(url,headers,function)

`参数`:

`url`: string

`headers`: object

`function`: function

示例：

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

`参数`:

`url`: string

`data`: object

`headers`: object

`function`: function

示例：

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

//或者

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

## 注意事项

headers中的key和value必须都是string类型，当data为object时为表单提交，header头部会加入content-type:application/x-www-form-urlencoded，如果提交content-type:application/json，需要确定data参数类型为string
