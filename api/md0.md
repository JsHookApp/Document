# global

简易调用的全局函数

## toast(message)

`parameter`:

`message`: string

## alert(message)

`parameter`:

`message`: string

## confirm(message,callback)

`parameter`:

`message`: string

`callback`: function

Example：

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

Returns 32-bit lowercase uuid

`return value`: string
