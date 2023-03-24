# 1.1介绍

jshook是对应用程序注入rhino/frida，你只需要会js就可以快速实现hook，并且支持java层和native层，降低开发人员的技术门槛，简化hook流程，`rhino`包含了xposed的api，主要用于java层的hook；`frida`注入后js可以完全访问内存，支持java层和native层。

与1.0相比，1.1使用`kotlin`重构，api全部重写，移除1.0版本中不规范的`LsposedMod`与`LspatchMod`这两个修改版，在root环境下可以安装jshook自制的Magisk模块，免root环境下使用`Lspatch`或者其他虚拟机环境。