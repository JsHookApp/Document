# Frequently Asked Questions

Some common problem solutions

## Where to download jshook related files

If you want to download some files offline, you can find them here

Download here: [https://github.com/JsHookApp/Download](https://github.com/JsHookApp/Download)

## How to support encrypted scripts

Currently, encrypted scripts can only be run using the `fridamod` framework

## Application crash

Some models will crash directly when injecting scripts in real time. You can turn off the hook service first, start the application first, wait a few seconds, and then start the injection when the hook service is turned on. Uncheck the script before testing to eliminate the script cause

## How to connect to frida-server

The default port number of frida-server provided by jshook is `28042/28043`

Connection example

```shell
#Port forwarding
adb forward tcp:28042 tcp:28042

#spawn
frida -H 127.0.0.1:28042 -f com.android.xxx -l test.js
#attach
frida -H 127.0.0.1:28042 -n com.android.xxx -l test.js
```

## How to connect frida-gadget

The port has been changed like frida-server

Connection example

```shell
#Port forwarding
adb forward tcp:28042 tcp:28042

#attach
frida -H 127.0.0.1:28042 Gadget -l test.js
```

## Turn on rendering and deactivate

Rendering enhancement is enabled by default, but not supported on some models. After cleaning the application data, turn off rendering enhancement in the activated state and then turn on rendering

## What is rendering enhancement

Rendering enhancement means using the underlying API for rendering directly without relying on the Android system. The Android system cannot sense its existence, so the performance is best in enhanced mode, and screen recording and screenshots cannot obtain rendering data

If rendering enhancement is not enabled, the Android system API is used to create rendering views, which will result in performance loss and be controlled by the system. Screen recording and screenshots can obtain rendering data

## How to make my model support rendering enhancement

Open the terminal (such as the terminal of the mt manager) and enter the following command
```shell
su
logcat|grep ImGui
```
The command means to continuously output a key log under the root user

Then enable rendering enhancement and send the terminal output log to the developer, who will update the module to be compatible with your model

## Server request failure in online service

The built-in online service may use the `github` link, which is not friendly to users in mainland China. You can prepare `vpn` access by yourself

## Cross-version update causes jshook to crash

For example, a cross-version update from 1.0.x to 1.1.x may cause incompatibility crashes due to large adjustments. Clear the application data, delete `/data/system/jshook` and `/data/adb/jshook`, and reinstall the activation module. Please note that you should back up the script and subscription before doing these operations.
