# app

Inspect and control the currently hooked application — its state, activities, paths, and more.

## app.isAppSystem()

Check if the app is a system application.

`Returns`: boolean

## app.isAppForeground()

Check if the app is in the foreground.

`Returns`: boolean

## app.exitApp()

Close the application.

## app.getAppInfo()

Get app information.

`Returns`: object

## app.openUrl(url)

Open a specified URL.

`Parameters`:

`url`: string

## app.startActivity(activity)

Start an Activity.

`Parameters`:

`activity`: Activity

## app.getActivityList()

Get the Activity stack list.

`Returns`: List\<Activity\>

## app.finishActivity(activity)

Finish an Activity.

`Parameters`:

`activity`: Activity

## app.finishToActivity(activity)

Finish to a specified Activity.

`Parameters`:

`activity`: Activity

## app.startHomeActivity()

Go to home screen.

## app.dpToPx(value)

Convert dp to px.

`Parameters`:

`value`: float

`Returns`: int

## app.pxToDp(value)

Convert px to dp.

`Parameters`:

`value`: float

`Returns`: int

## app.getInternalAppDataPath()

Get internal app data path.

`Returns`: string

## app.getExternalAppDataPath()

Get external app data path.

`Returns`: string

## app.getExternalAppObbPath()

Get external app OBB path.

`Returns`: string

## app.getExternalStoragePath()

Get external storage path.

`Returns`: string
