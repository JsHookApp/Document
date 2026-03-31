# Installation & Activation

## Prerequisites

Your device must have root access. Any of the following root frameworks are supported:

- `Magisk` [https://github.com/topjohnwu/Magisk](https://github.com/topjohnwu/Magisk)
- `KernelSU` [https://github.com/tiann/KernelSU](https://github.com/tiann/KernelSU)
- `APatch` [https://github.com/bmax121/APatch](https://github.com/bmax121/APatch)

## Activation Steps

1. Install the JsHook app
2. Open JsHook, tap the **Activate** button on the home page
3. Grant root permission when prompted
4. Wait for activation to complete — the app will automatically deploy runtime files and start the background service
5. Once activated, the home page will show "Activated" status with Daemon process information

> During activation, JsHook automatically performs the following:
> - Deploys runtime files to `/data/adb/jshook/`
> - Releases the kernel driver module matching the current kernel version
> - Starts the background Daemon service
> - Fixes file permissions

## Getting Started

After activation:

1. Select the target app from the app list
2. Choose a hook framework
3. Check the scripts you want to execute
4. Enable the hook service
5. Open the target app — scripts will run automatically

### Hook Framework Comparison

| Framework | Description |
|-----------|-------------|
| **fridamod** | Recommended. Embedded Frida with full jscore API support, kernel mode, ImGui rendering and encrypted scripts |
| **fridainject** | Uses frida-server injection, supports jscore API |
| **fridagadget** | Uses frida-gadget config injection, supports jscore API |

## Virtual Machine

Use `vmos` or `LightSpeed VM` or similar products. The activation process is the same as above.

## Emulator

Get root access in the emulator, then follow the activation steps above.
