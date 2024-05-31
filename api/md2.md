# app

用于获取当前hook应用的基本信息

## app.isAppSystem()

判断 App 是否是系统应用

`返回值`: boolean

## app.isAppForeground()

判断 App 是否处于前台

`返回值`: boolean

## app.exitApp()

关闭应用

## app.getAppInfo()

获取 App 信息

`返回值`: object

## app.openUrl(url)

打开指定网址

`参数`:

`url`: string 网址

## app.startActivity(activity)

启动 Activity

`参数`:

`activity`: Activity

## app.getActivityList()

获取 Activity 栈链表

`返回值`: List<Activity>

## app.finishActivity(activity)

结束 Activity

`参数`:

`activity`: Activity

## app.finishToActivity(activity)

结束到指定 Activity

`参数`:

`activity`: Activity

## app.startHomeActivity()

回到桌面

## app.dpToPx(value)

dp转px

`参数`:

`value`: float

`返回值`: int

## app.pxToDp(value)

px转dp

`参数`:

`value`: float

`返回值`: int

## app.getInternalAppDataPath()

获取内存应用数据路径

`返回值`: string

## app.getExternalAppDataPath()

获取外存应用数据路径

`返回值`: string

## app.getExternalAppObbPath()

获取外存应用 OBB 路径

`返回值`: string

## app.getExternalStoragePath()

获取外存路径

`返回值`: string
