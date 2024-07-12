# app

Used to get the basic information of the current hook application

## app.isAppSystem()

Determine whether the App is a system application

`Return value`: boolean

## app.isAppForeground()

Determine whether the App is in the foreground

`Return value`: boolean

## app.exitApp()

Close the application

## app.getAppInfo()

Get App information

`Return value`: object

## app.openUrl(url)

Open the specified URL

`Parameter`:

`url`: string URL

## app.startActivity(activity)

Start Activity

`Parameter`:

`activity`: Activity

## app.getActivityList()

Get the Activity stack list

`Return value`: List<Activity>

## app.finishActivity(activity)

End Activity

`Parameter`:

`activity`: Activity

## app.finishToActivity(activity)

End to the specified Activity

`Parameters`:

`activity`: Activity

## app.startHomeActivity()

Return to the desktop

## app.dpToPx(value)

dp to px

`Parameters`:

`value`: float

`Return value`: int

## app.pxToDp(value)

px to dp

`Parameters`:

`value`: float

`Return value`: int

## app.getInternalAppDataPath()

Get the internal memory application data path

`Return value`: string

## app.getExternalAppDataPath()

Get the external storage application data path

`Return value`: string

## app.getExternalAppObbPath()

Get the external storage application OBB path

`Return value`: string

## app.getExternalStoragePath()

Get the external storage path

`Return value`: string
