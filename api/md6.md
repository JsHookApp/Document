# device

Used to obtain basic information of the current device

## device.isAdbEnabled()

Determine whether the device ADB is available

`Return value`: boolean

## device.getSDKVersionName()

Get the device system version number

`Return value`: string

## device.getSDKVersionCode()

Get the device system version code

`Return value`: int

## device.getAndroidID()

Get the device AndroidID

`Return value`: string

## device.getMacAddress()

Get the device MAC address

`Return value`: string

## device.getManufacturer()

Get the device manufacturer

`Return value`: string

## device.getModel()

Get the device model

`Return value`: string

## device.getABIs()

Get the device ABIs

`Return value`: string

## device.isTablet()

Determine whether it is a tablet

`Return value`: boolean

## device.isDevelopmentSettingsEnabled()

Whether the developer options are turned on

`Return value`: boolean

## device.getScreenWidth()

Get the width of the screen (unit: px)

`Return value`: int

## device.getScreenHeight()

Get the height of the screen (unit: px)

`Return value`: int

## device.getScreenDensity()

Get the screen density

`Return value`: float

## device.getScreenDensityDpi()

Get the screen density DPI

`Return value`: int

## device.isLandscape()

Determine whether the screen is horizontal

`Return value`: boolean

## device.isPortrait()

Determine whether the screen is vertical

`Return value`: boolean

## device.screenShot(activity)

Screenshot

`Parameters`:

`activity`: Activity

`Return value`: Bitmap

## device.setClipboard(data)

Set the clipboard content

`Parameters`:

`data`: string

## device.getClipboard()

Get the clipboard content

`Return value`: string
