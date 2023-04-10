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

```javascript
XposedBridge.hookAllMethods(XposedHelpers.findClass("android.app.Application", runtime.classLoader), "onCreate", XC_MethodReplacement({
    replaceHookedMethod: function (param) {
        console.log('hook');
        return XposedBridge.invokeOriginalMethod(param.method, param.thisObject, param.args);
    }
}));
```

```javascript
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

## XposedHelpers.findClass(className,classLoader)

```javascript
XposedHelpers.findClass('com.test.test',runtime.classLoader);
```

## XposedBridge.hookAllConstructors(hookClass,callback)

```javascript
XposedBridge.hookAllConstructors(XposedHelpers.findClass('com.test.test',runtime.classLoader),XC_MethodHook({
    beforeHookedMethod: function (param) {
        console.log('hook before');
    },
    afterHookedMethod: function (param) {
        console.log('hook after');
    }
}));
```

## XposedHelpers.findAndHookConstructor(clazz,parameterTypesAndCallback)

```javascript
XposedHelpers.findAndHookConstructor(XposedHelpers.findClass('com.test.test',runtime.classLoader),'java.lang.String','java.lang.String',XC_MethodHook({
    beforeHookedMethod: function (param) {
        console.log('hook before');
    },
    afterHookedMethod: function (param) {
        console.log('hook after');
    }
}));
```

## XposedHelpers.findAndHookConstructor(className,classLoader,parameterTypesAndCallback)

```javascript
XposedHelpers.findAndHookConstructor('com.test.test',runtime.classLoader,'java.lang.String','java.lang.String',XC_MethodHook({
    beforeHookedMethod: function (param) {
        console.log('hook before');
    },
    afterHookedMethod: function (param) {
        console.log('hook after');
    }
}));
```

## XposedBridge.hookAllMethods(hookClass,methodName,callback)

```javascript
XposedBridge.hookAllMethods(XposedHelpers.findClass('com.test.test',runtime.classLoader),'method',XC_MethodHook({
    beforeHookedMethod: function (param) {
        console.log('hook before');
    },
    afterHookedMethod: function (param) {
        console.log('hook after');
    }
}));
```

## XposedBridge.hookMethod(hookMethod,callback)

```javascript
XposedBridge.hookMethod(param.method,XC_MethodHook({
    beforeHookedMethod: function (param) {
        console.log('hook before');
    },
    afterHookedMethod: function (param) {
        console.log('hook after');
    }
}));
```

## XposedHelpers.setStaticObjectField(clazz,fieldName,value)

```javascript
XposedHelpers.setStaticObjectField(XposedHelpers.findClass('com.test.test',runtime.classLoader),'name','test');
```

## XposedHelpers.setObjectField(obj,fieldName,value)

```javascript
XposedHelpers.setObjectField(param.thisObject,'name','test');
```

## XposedHelpers.getStaticObjectField(clazz,fieldName)

```javascript
XposedHelpers.getStaticObjectField(XposedHelpers.findClass('com.test.test',runtime.classLoader),'name');
```

## XposedHelpers.getObjectField(clazz,fieldName)

```javascript
XposedHelpers.getObjectField(param.thisObject,'name');
```

## XposedHelpers.callMethod(obj,methodName,args)

```javascript
XposedHelpers.callMethod(param.thisObject,'method','123','456');
```

## XposedHelpers.callStaticMethod(clazz,methodName,parameterTypes,args)

```javascript
XposedHelpers.callStaticMethod(XposedHelpers.findClass('com.test.test',runtime.classLoader),'method','123','456');
```

## XposedBridge.invokeOriginalMethod(method,thisObject,args)

```javascript
XposedBridge.invokeOriginalMethod(param.method,param.thisObject,param.args);
```

## ...

更多同上精简的方式调用即可

## 如何hook加壳的应用

以下是常用的示例，有一些企业壳做了特殊处理，可能不适用

```javascript
XposedBridge.hookAllMethods(XposedHelpers.findClass('android.app.ActivityThread', runtime.classLoader), 'performLaunchActivity', XC_MethodHook({
    beforeHookedMethod: function (param) {
        console.log('hook before');
    },
    afterHookedMethod: function (param) {
        console.log('hook after');
        var mInitialApplication = XposedHelpers.getObjectField(param.thisObject, 'mInitialApplication');
        var classLoader = XposedHelpers.callMethod(mInitialApplication, 'getClassLoader');
        XposedBridge.hookAllMethods(XposedHelpers.findClass('com.test.test', classLoader), 'test', XC_MethodHook({
            beforeHookedMethod: function (param) {
                console.log('hook before');
            },
            afterHookedMethod: function (param) {
                console.log('hook after');
            }
        }));
    }
}));
```
