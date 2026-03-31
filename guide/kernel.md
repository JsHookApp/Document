# 内核驱动模式

内核驱动模式允许 JsHook 在不注入目标应用的情况下，通过内核级别的内存操作来读写目标进程的内存数据。

## 工作原理

内核模式下，JsHook 不注入目标应用进程，而是创建一个独立的"旁观进程"（fake process），在旁观进程中运行 Frida 脚本。通过内核驱动模块直接访问目标进程的内存空间。

优势：
- 不修改目标应用进程，更难被反作弊检测
- 支持读写目标进程的任意内存
- 旁观进程独立运行，不影响目标应用稳定性

## 前置条件

### 1. 内核版本兼容

内核驱动需要与设备的 Linux 内核版本匹配。JsHook 在激活时会自动检测内核版本并释放对应的 `.ko` 模块。

查看内核版本：
```shell
adb shell uname -r
```

### 2. Root 权限

必须拥有 root 权限，支持以下 root 方案：
- **Magisk** — 推荐
- **KernelSU**
- **APatch**

### 3. SELinux 策略

部分设备需要将 SELinux 设为宽容模式：
```shell
adb shell su -c setenforce 0
```

### 4. JsHook 已激活

确保 JsHook 已通过 Magisk/KernelSU 模块安装并激活。

## 启用内核模式

1. 打开 JsHook 应用
2. 在目标应用的 Hook 配置中选择 **fridamod** 框架
3. 开启 **内核模式** 开关
4. 分配需要执行的脚本
5. 启动目标应用

## 内核模式下的 API 限制

内核模式下，脚本运行在旁观进程中，**不在目标应用进程内**，因此：

### ✅ 可用 API

| API | 说明 |
|-----|------|
| `kernel.getModuleBase(name)` | 获取目标进程中 SO 库的基地址 |
| `kernel.readDword(address)` | 读取目标进程内存（整数） |
| `kernel.readFloat(address)` | 读取目标进程内存（浮点数） |
| `kernel.writeDword(address, value)` | 写入目标进程内存（整数） |
| `kernel.writeFloat(address, value)` | 写入目标进程内存（浮点数） |
| `memory.*` | 通过 daemon IPC 读写目标进程内存 |
| `console.log()` | 日志输出 |
| `runtime.*` | 运行时信息（部分字段） |
| `storage.*` | 本地数据存储 |
| `modmenu.*` | Mod 菜单（通过 daemon IPC） |
| `moddraw.*` | ImGui 绘制 |

### ❌ 不可用 API

| API | 原因 |
|-----|------|
| `Java.use()` / `Java.perform()` | 旁观进程没有加载目标应用的类 |
| `Interceptor.*` | 无法 hook 目标进程的函数 |
| `app.*` | 依赖目标应用上下文 |
| `view.*` | 依赖目标应用 UI 线程 |
| `toast()` / `alert()` | 依赖 daemon Binder（内核模式下可能不可用） |
| `http.*` | 依赖 daemon IPC |

> **提示**：使用 `runtime.isKernel` 判断当前是否在内核模式下运行，可以在脚本中做条件分支。

## 示例脚本

```javascript
if (runtime.isKernel) {
    // 内核模式，使用 kernel API 操作目标进程内存
    var base = kernel.getModuleBase('libil2cpp.so');
    console.log('libil2cpp base: ' + base);
    
    if (base && base !== '0x0') {
        var health = kernel.readFloat(
            '0x' + (parseInt(base, 16) + 0x1A2B3C4).toString(16)
        );
        console.log('Health: ' + health);
    }
} else {
    // 普通模式，使用 Frida API hook
    Java.perform(function () {
        // ...
    });
}
```

## 故障排查

### 内核驱动加载失败

1. 确认内核版本兼容：`uname -r`
2. 检查 SELinux：`getenforce`（如果返回 `Enforcing`，尝试 `setenforce 0`）
3. 检查 root 权限是否正常
4. 查看 dmesg 日志：`dmesg | grep jshook`

### getModuleBase 返回 0x0

1. 确认目标应用已启动且目标 SO 已加载
2. SO 名称需要精确匹配（区分大小写）
3. 检查内核驱动是否正常运行：通过 MCP 工具 `kernel_status` 查看

### 旁观进程启动失败

1. 检查 `/data/adb/jshook/.kernel/` 目录权限
2. 确认 `app_process` 可执行
3. 查看内核日志：`cat /data/adb/jshook/.kernel/kernel_*.log`
