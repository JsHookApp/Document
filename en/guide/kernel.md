# Kernel Driver Mode

Kernel driver mode allows JsHook to read/write target process memory through kernel-level operations without injecting into the target application.

## How It Works

In kernel mode, JsHook doesn't inject into the target app process. Instead, it creates an independent "spectator process" (fake process) that runs Frida scripts. It accesses the target process memory directly through the kernel driver module.

Advantages:
- Doesn't modify the target app process, making it harder for anti-cheat to detect
- Supports reading/writing arbitrary memory of the target process
- The spectator process runs independently without affecting target app stability

## Prerequisites

### 1. Kernel Version Compatibility

The kernel driver must match the device's Linux kernel version. JsHook automatically detects the kernel version during activation and loads the corresponding `.ko` module.

Check kernel version:
```shell
adb shell uname -r
```

### 2. Root Access

Root access is required. Supported root frameworks:
- **Magisk** — Recommended
- **KernelSU**
- **APatch**

### 3. SELinux Policy

Some devices may require setting SELinux to permissive mode:
```shell
adb shell su -c setenforce 0
```

### 4. JsHook Activated

Ensure JsHook has been installed and activated via the Magisk/KernelSU module.

## Enable Kernel Mode

1. Open JsHook app
2. In the target app's hook configuration, select the **fridamod** framework
3. Enable the **Kernel Mode** toggle
4. Assign scripts to execute
5. Launch the target app

## API Limitations in Kernel Mode

In kernel mode, scripts run in the spectator process, **not inside the target app process**, therefore:

### ✅ Available APIs

| API | Description |
|-----|-------------|
| `kernel.getModuleBase(name)` | Get SO library base address in target process |
| `kernel.readDword(address)` | Read target process memory (integer) |
| `kernel.readFloat(address)` | Read target process memory (float) |
| `kernel.writeDword(address, value)` | Write target process memory (integer) |
| `kernel.writeFloat(address, value)` | Write target process memory (float) |
| `memory.*` | Read/write target process memory via daemon IPC |
| `console.log()` | Log output |
| `runtime.*` | Runtime information (partial) |
| `storage.*` | Local data storage |
| `modmenu.*` | Mod menu (via daemon IPC) |
| `moddraw.*` | ImGui drawing |

### ❌ Unavailable APIs

| API | Reason |
|-----|--------|
| `Java.use()` / `Java.perform()` | Spectator process doesn't have target app classes loaded |
| `Interceptor.*` | Cannot hook target process functions |
| `app.*` | Depends on target app context |
| `view.*` | Depends on target app UI thread |
| `toast()` / `alert()` | Depends on daemon Binder (may be unavailable in kernel mode) |
| `http.*` | Depends on daemon IPC |

> **Tip**: Use `runtime.isKernel` to check if running in kernel mode, and create conditional branches in your scripts.

## Example Script

```javascript
if (runtime.isKernel) {
    // Kernel mode — use kernel API to operate target process memory
    var base = kernel.getModuleBase('libil2cpp.so');
    console.log('libil2cpp base: ' + base);
    
    if (base && base !== '0x0') {
        var health = kernel.readFloat(
            '0x' + (parseInt(base, 16) + 0x1A2B3C4).toString(16)
        );
        console.log('Health: ' + health);
    }
} else {
    // Normal mode — use Frida API to hook
    Java.perform(function () {
        // ...
    });
}
```

## Troubleshooting

### Kernel driver fails to load

1. Verify kernel version compatibility: `uname -r`
2. Check SELinux: `getenforce` (if `Enforcing`, try `setenforce 0`)
3. Verify root access is working
4. Check dmesg logs: `dmesg | grep jshook`

### getModuleBase returns 0x0

1. Confirm target app is running and the target SO is loaded
2. SO name must be an exact match (case-sensitive)
3. Verify kernel driver is running: use MCP tool `kernel_status`

### Spectator process fails to start

1. Check `/data/adb/jshook/.kernel/` directory permissions
2. Confirm `app_process` is executable
3. Check kernel logs: `cat /data/adb/jshook/.kernel/kernel_*.log`
