# 常见问题

常见的一些问题处理方案

## jshook相关文件在哪下载

如果你想里离线下载一些文件，可以在这里找到

在这里下载: [https://github.com/JsHookApp/Download](https://github.com/JsHookApp/Download)

## 加密脚本如何支持

目前加密脚本只能使用`fridamod`框架运行

## 应用闪退

部分机型实时注入脚本会直接发生闪退情况，你可以先关闭hook服务，先启动应用，等待几秒后在开启hook服务会途中开始注入，在测试之前先取消勾选脚本，排除脚本原因

## frida-server如何连接

jshook提供的frida-server默认端口号为`28042/28043`

连接示例

```shell
#端口转发
adb forward tcp:28042 tcp:28042

#spawn
frida -H 127.0.0.1:28042 -f com.android.xxx -l test.js
#attach
frida -H 127.0.0.1:28042 -n com.android.xxx -l test.js
```

## frida-gadget如何连接

与frida-server一样更改了端口

连接示例

```shell
#端口转发
adb forward tcp:28042 tcp:28042

#attach
frida -H 127.0.0.1:28042 Gadget -l test.js
```

## 开启渲染掉激活

渲染增强默认是开启的，部分机型不支持，清理应用数据后在激活状态下先关闭渲染增强在开启渲染

## 什么是渲染增强

渲染增强指不依赖android系统的情况下直接使用底层api进行渲染，android系统无法感知存在，所以在增强模式下性能最好，且屏幕录制和截屏无法获取到渲染数据

没有开启渲染增强则使用android系统的api创建渲染试图，性能会有损失，且受系统管控，屏幕录制和截屏可以获取到渲染数据

## 如何让我的机型支持渲染增强

打开终端(例如mt管理器的终端)输入以下命令
```shell
su
logcat|grep ImGui
```
命令的意思是在root用户下持续输出某个关键日志

然后开启渲染增强把终端输出的日志发给开发者，开发者会更新模块来兼容你的机型

## 在线服务出现服务器请求失败

内置的在线服务可能使用了`github`链接，对于中国大陆用户访问不友好，可以自行准备`vpn`访问

## 跨大版本更新导致jshook闪退

例如从1.0.x更新到1.1.x这种跨大版本更新因为调整过大导致不兼容闪退，清空应用数据，删除`/data/system/jshook`和`/data/adb/jshook`，重新安装激活模块，注意，做这些操作之前请先备份脚本和订阅
