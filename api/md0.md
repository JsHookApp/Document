# global

Global function for easy calling

## toast(message)

`parameters`:

`message`: string

## alert(message)

`parameters`:

`message`: string

## confirm(message,callback)

`parameters`:

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

Returns 32-bit lowercase uuid

`return value`: string
