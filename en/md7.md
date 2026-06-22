# FAQ

Solutions to some of the problems you may run into.

## Where can I download JsHook's files?

If you'd like to download JsHook's files for offline use, you can find them here:

[https://github.com/JsHookApp/Download](https://github.com/JsHookApp/Download)

## How are encrypted scripts supported?

For now, encrypted scripts can only be run with the `fridamod` framework.

## The app crashes

On some devices, injecting scripts in real time causes an immediate crash. To work around this, disable the hook service first, launch the target app, wait a few seconds, then enable the hook service so that injection happens mid-run. Before you start testing, uncheck all scripts so you can rule out a faulty script as the cause.

## How do I connect to frida-server?

JsHook's frida-server listens on ports `28042/28043` by default.

Example:

```shell
# Port forwarding
adb forward tcp:28042 tcp:28042

# spawn
frida -H 127.0.0.1:28042 -f com.android.xxx -l test.js
# attach
frida -H 127.0.0.1:28042 -n com.android.xxx -l test.js
```

## How do I connect to frida-gadget?

The same as frida-server, just on the changed port.

Example:

```shell
# Port forwarding
adb forward tcp:28042 tcp:28042

# attach
frida -H 127.0.0.1:28042 Gadget -l test.js
```

## Enabling rendering drops the activation

Enhanced rendering is enabled by default, but some devices don't support it. Clear the app's data, and then — while activated — turn enhanced rendering off and back on again.

## What is Enhanced Rendering?

Enhanced rendering draws directly through low-level APIs without relying on the Android system. The system has no idea it exists, so this mode delivers the best performance, and the rendered content cannot be captured by screen recording or screenshots.

With enhanced rendering disabled, JsHook falls back to the Android system's APIs to create rendering views. This costs some performance, is subject to system restrictions, and the rendered content *can* be captured by screen recording and screenshots.

## How do I get enhanced rendering working on my device?

Open a terminal (for example, the terminal in MT Manager) and run:

```shell
su
logcat|grep ImGui
```

This continuously prints the relevant logs as the root user.

Now enable enhanced rendering and send the terminal output to the developer, who will update the module to add support for your device.

## "Server request failed" with the online services

The built-in online services sometimes rely on `GitHub` links, which are hard to reach from mainland China. If you're affected, use a `VPN` to access them.

## JsHook crashes after a major version update

A jump across major versions — for example, from 1.0.x to 1.1.x — can involve changes large enough to break compatibility and crash the app. To recover, clear the app's data, delete `/data/system/jshook` and `/data/adb/jshook`, and reactivate. **Back up your scripts and subscriptions before you do this.**
