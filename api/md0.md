# global

简易调用的全局函数

## toast(message)

`参数`:

`message`: string

## alert(message)

`参数`:

`message`: string

## confirm(message,callback)

`参数`:

`message`: string

`callback`: function

示例：

```javascript
confirm('is ok?', {
    ok: function () {
        //...
    },
    cancel: function () {
        //...
    }
})
```

## uuid()

返回32位小写uuid

`返回值`: string

## setTimeout(function,time)

`参数`:

`function`: function

`time`: int 毫秒

`返回值`: int 事件标识

示例：

```javascript
setTimeout(function () {
    //...
}, 100);
```

## clearTimeout(id)

`参数`:

`id`: int 事件标识

## setInterval(function,time)

`参数`:

`function`: function

`time`: int 毫秒

`返回值`: int 事件标识

示例：

```javascript
setInterval(function () {
    //...
}, 100);
```

## clearInterval(id)

`参数`:

`id`: int 事件标识
