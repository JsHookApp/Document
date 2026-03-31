# FAQ

Common troubleshooting solutions.

## Where to download JsHook files?

If you want to download files offline:

Download here: [https://github.com/JsHookApp/Download](https://github.com/JsHookApp/Download)

## Encrypted script support

Currently encrypted scripts can only run with the `fridamod` framework.

## App crashes

Some devices may crash when injecting scripts in real-time. You can first disable the hook service, launch the target app, wait a few seconds, then enable the hook service to inject mid-run. Before testing, uncheck all scripts to rule out script-related issues.

## How to connect frida-server?

The default port for JsHook's frida-server is `28042/28043`.

Connection example:

```shell
# Port forwarding
adb forward tcp:28042 tcp:28042

# spawn
frida -H 127.0.0.1:28042 -f com.android.xxx -l test.js
# attach
frida -H 127.0.0.1:28042 -n com.android.xxx -l test.js
```

## How to connect frida-gadget?

Same as frida-server with the modified port.

Connection example:

```shell
# Port forwarding
adb forward tcp:28042 tcp:28042

# attach
frida -H 127.0.0.1:28042 Gadget -l test.js
```

## Enabling rendering causes deactivation

Enhanced rendering is enabled by default. Some devices don't support it. Clear the app data, then while activated, disable enhanced rendering first before re-enabling it.

## What is Enhanced Rendering?

Enhanced rendering uses low-level APIs to render directly without depending on the Android system. The Android system is unaware of its existence, so performance is optimal in this mode, and screen recording/screenshots cannot capture the rendered content.

Without enhanced rendering, Android system APIs are used to create rendering views, which may have performance overhead and are subject to system controls — screen recording and screenshots can capture the rendered content.

## How to make my device support Enhanced Rendering?

Open a terminal (e.g., MT Manager terminal) and enter:
```shell
su
logcat|grep ImGui
```
This command continuously outputs relevant logs under root user.

Then enable enhanced rendering and send the terminal output to the developer, who will update the module to support your device.

## "Server request failed" in online services

Built-in online services may use `GitHub` links, which are not accessible in some regions. You may need a `VPN` for access.

## Major version update causes JsHook crash

For example, updating from 1.0.x to 1.1.x may cause crashes due to incompatible changes. Clear app data, delete `/data/system/jshook` and `/data/adb/jshook`, then reactivate. **Back up your scripts and subscriptions before doing this.**
