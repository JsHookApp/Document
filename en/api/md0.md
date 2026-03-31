# global

Simple global functions for quick access.

## toast(message)

`Parameters`:

`message`: string

## alert(message)

`Parameters`:

`message`: string

## confirm(message,callback)

`Parameters`:

`message`: string

`callback`: function

Example:

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

Returns a 32-character lowercase UUID.

`Returns`: string
