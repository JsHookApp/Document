# device

用于获取当前设备的基础信息

## device.isAdbEnabled()

判断设备 ADB 是否可用

`返回值`: boolean

## device.getSDKVersionName()

获取设备系统版本号

`返回值`: string

## device.getSDKVersionCode()

获取设备系统版本码

`返回值`: int

## device.getAndroidID()

获取设备 AndroidID

`返回值`: string

## device.getMacAddress()

获取设备 MAC 地址

`返回值`: string

## device.getManufacturer()

获取设备厂商

`返回值`: string

## device.getModel()

获取设备型号

`返回值`: string

## device.getABIs()

获取设备 ABIs

`返回值`: string

## device.isTablet()

判断是否是平板

`返回值`: boolean

## device.isDevelopmentSettingsEnabled()

开发者选项是否打开

`返回值`: boolean

## device.getScreenWidth()

获取屏幕的宽度（单位：px）

`返回值`: int

## device.getScreenHeight()

获取屏幕的高度（单位：px）

`返回值`: int

## device.getScreenDensity()

获取屏幕密度

`返回值`: float

## device.getScreenDensityDpi()

获取屏幕密度 DPI

`返回值`: int

## device.isLandscape()

判断是否横屏

`返回值`: boolean

## device.isPortrait()

判断是否竖屏

`返回值`: boolean

## device.screenShot(activity)

截屏

`参数`:

`activity`: Activity

`返回值`: Bitmap

## device.setClipboard(data)

设置剪贴板内容

`参数`:

`data`: string

## device.getClipboard()

获取剪贴板内容

`返回值`: string
