# Self-built warehouse

If you need to build your own script warehouse, you only need to provide the json file address in the following format. Configure the address in the menu in the upper right corner of the warehouse interface. `Fields that are not needed can be null or deleted`

## List format

In the list format, the warehouse only displays the script list information, and will not display other warehouse information. If you need more functions, please refer to the complete format below

```json
[
{
"author": "",
"markdown": "",
"ctime": "",
"source": "",
"id": "",
"title": "",
"type": "",
"version": "",
"url": "",
"desc": "",
"down_count": 0
}
]
```

Field description:

`author`: string Displays the name of the script author

`markdown`: string Detailed description of the markdown file url address

`ctime`: string Script creation time, format: 0000-00-00

`source`: string Script source URL address, such as the script's open source github address, non-script download address

`id`: string Script unique identifier, can use uuid

`title`: string Script name

`type`: string Two values ​​rhino or frida Tell the user what script this is

`version`: string Version number For example 1.0.0

`url`: string Script download address

`desc`: string Script description, controlled within 30 words, simple description, detailed description written in markdown

`down_count`: int Script download count

## Complete format

The warehouse in the complete format can be used for more functions

```json
{
"name": "",
"icon": "",
"list": "",
"push": "",
"markdown": "",
"group_qq": "",
"group_tg": "",
"user_count": 0
}
```

`name`: string Warehouse name

`icon`: string URL address of warehouse icon

`list`: string URL address in list format

`push`: string URL address of push configuration

`markdown`: string URL address of markdown file with detailed warehouse information

`group_qq`: string QQ group key is available here [https://qun.qq.com/join.html](https://qun.qq.com/join.html)

`group_tg`: string For example, if the group link is https://t.me/jshookgroup, fill in jshookgroup

`user_count`: int Number of warehouse users

### Push configuration

If the warehouse uses the full format and needs to use push, the json format of the push file is as follows

```json
[
{
"id": "",
"title": "",
"args": "",
"action": ""
}
]
```

Only when jshook settings allow receiving message notifications can push content be received

In order not to interfere with users, pushes will not be received in real time. There are trigger conditions. When the user opens jshook or other applications that inject jshook services, push content will be pulled. If the user has not received the start message notification, the id will be used to determine if the user has not received it

`id`: string Push unique identifier

`title`: string Message title

`args`: string When action is markdown, fill in the markdown file URL address

`action`: string Jump type, fixed value is markdown

## DeepLink

In html, you can use the following method to jump to jshook to add warehouse subscriptions. In fact, the url is the subscription url address of the warehouse

```html
<a href="jshook://store?url=http://xxxxx.com">Add warehouse subscription</>

```
