# xposed

使用rhino调用xposed相关api的示例

首先你需要知道java如何调用xposed相关api，进入这里查看说明:

[https://api.xposed.info/reference/packages.html](https://api.xposed.info/reference/packages.html)


而jshook中的rhino框架提供了以下xposed的api:

`XposedBridge`

`XposedHelpers`

`AndroidAppHelper`

`XC_MethodHook`

`XC_MethodReplacement`

现在你只需要使用rhino语法用简单的方式去实现，关于rhino语法教程，可以进入这里查看说明：

[https://p-bakker.github.io/rhino/tutorials/scripting_java/](https://p-bakker.github.io/rhino/tutorials/scripting_java/)

以下是常见的一个示例：

```js
XposedBridge.hookAllMethods(XposedHelpers.findClass("android.app.Application", runtime.classLoader), "onCreate", XC_MethodReplacement({
    replaceHookedMethod: function (param) {
        console.log('hook');
        return XposedBridge.invokeOriginalMethod(param.method, param.thisObject, param.args);
    }
}));
```

```js
XposedBridge.hookAllMethods(XposedHelpers.findClass("android.app.Application", runtime.classLoader), "onCreate", XC_MethodHook({
    beforeHookedMethod: function (param) {
        console.log('hook before');
    },
    afterHookedMethod: function (param) {
        console.log('hook after');
    }
}));
```

从示例中我们可以看到，几乎和java的写法一致，只是进行了简化
