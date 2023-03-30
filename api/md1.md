# runtime

用于获取当前hook运行时相关基础信息

## runtime.jsContent

获取当前注入的脚本内容，注意，如果是加密脚本，获取的不会是解密后的文本

`返回值`: string

## runtime.appInfo

`返回值`: ApplicationInfo

你可以通过这个获取到`dataDir`私有路径

```js
console.log(runtime.appInfo.dataDir);
```

## runtime.packageName

`返回值`: string

## runtime.processName

`返回值`: string

## runtime.classLoader

`返回值`: ClassLoader

## runtime.isFirstApplication

`返回值`: boolean

## runtime.coreVersionCode

获取当前jshook的版本号

`返回值`: int

## runtime.coreType

获取当前注入的类型(1:rhino 2:frida)

`返回值`: int
