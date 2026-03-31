# 安装与激活

## 前置条件

你需要确保你的手机已经拥有 root 权限，支持以下任意一种 root 方案：

- `Magisk` [https://github.com/topjohnwu/Magisk](https://github.com/topjohnwu/Magisk)
- `KernelSU` [https://github.com/tiann/KernelSU](https://github.com/tiann/KernelSU)
- `APatch` [https://github.com/bmax121/APatch](https://github.com/bmax121/APatch)

## 激活步骤

1. 安装 JsHook 应用
2. 打开 JsHook，点击首页的 **激活** 按钮
3. 授予 root 权限弹窗
4. 等待激活完成，应用会自动部署运行时文件并启动后台服务
5. 激活成功后首页状态会显示为"已激活"，并展示 Daemon 进程信息

> 激活过程中 JsHook 会自动完成以下工作：
> - 释放运行时文件到 `/data/adb/jshook/`
> - 释放匹配当前内核版本的驱动模块
> - 启动后台 Daemon 服务
> - 修复文件权限

## 开始使用

激活成功后：

1. 在应用列表中选择要 hook 的目标应用
2. 选择 hook 框架
3. 勾选需要执行的脚本
4. 开启 hook 服务
5. 打开目标应用，脚本即自动运行

### hook 框架说明

| 框架 | 说明 |
|------|------|
| **fridamod** | 推荐使用。内嵌 frida，支持完整的 jscore API，支持内核模式、ImGui 渲染和加密脚本 |
| **fridainject** | 使用 frida-server 注入，支持 jscore API |
| **fridagadget** | 使用 frida-gadget 配置注入，支持 jscore API |

## 虚拟机环境

使用 `vmos` 或者 `光速虚拟机` 等类似产品，操作方式同上

## 模拟器环境

在模拟器中获取 root 权限后，按照上面的激活步骤操作即可
