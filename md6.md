# 安装

这里例举几个常见的安装激活方式

## 真机root环境激活

你需要确保你的手机已经拥有root权限，并且已经安装`magisk`，[https://github.com/topjohnwu/Magisk](https://github.com/topjohnwu/Magisk)

jshook属于xp模块，一般情况下使用`lsposed`进行激活，[https://github.com/LSPosed/LSPosed](https://github.com/LSPosed/LSPosed)

安装lsposed后在模块中启用jshook，并勾选`系统框架`，重启手机后完成激活

另：如果你没有lsposed，也可以直接安装jshook的面具模块进行激活，jshook应用首页点击`安装magisk模块`前两个模块用于激活，同时，`支持与lsposed共存`

## 真机免root环境激活

如果你手机无法root，可以尝试使用`lspatch` [https://github.com/LSPosed/LSPatch](https://github.com/LSPosed/LSPatch)

lspatch激活xp模块的方式是给目标应用进行修补`过签名验证`并修改`程序入口`，入口处会加入注入xposed框架以及调用lsp相关服务

安装lspatch后jshook会显示激活

安装完lspatch后你需要先将原应用`提取成apk文件`，可以使用`mt管理器`进行操作，lspatch中点击`管理`右下角`+号`新建修补，选择apk文件，修补完成后，用mt管理器找到修补后的apk文件，并安装，安装完成后在lspatch的管理中即可看到被修补成功的应用，点击这个应用，会出现菜单，选择`模块作用域`，勾选jshook即可完成激活

## 虚拟机环境激活

使用`vmos`或者`光速虚拟机`等类似产品进行安装激活操作，操作方式同上两种流程一样

## 模拟器环境激活

这里使用`夜神模拟器`来做示例，在这里下载 [https://www.yeshen.com/](https://www.yeshen.com/)

添加模拟器选择`android9`，可以先安装`magisk`，[在这里](md7) 下载`Magisk Terminal Emulator.apk`直接拖到模拟器中会自动安装，打开该应用依次输入以下指令即可完成安装magisk:

```shell
inmagisk
y
1
a
1
```

完成后重启模拟器你可以安装上面root环境激活的方式继续操作
