# 自建仓库

需要搭建属于自己的脚本仓库，只需要提供以下格式的json文件地址即可，仓库界面右上角菜单中配置地址，`字段不需要的可以为null或者删除该字段`

## 列表格式

列表格式下仓库只显示脚本列表信息，不会显示仓库其他信息，如果需要更多的功能，请参考下方的完整格式

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

字段说明：

`author`: string 显示脚本作者名称

`markdown`: string 详细说明markdown文件url地址

`ctime`: string 脚本创建时间，格式为：0000-00-00

`source`: string 脚本来源url地址，比如脚本的开源github地址，非脚本的下载地址

`id`: string 脚本唯一标识，可以用uuid

`title`: string 脚本名称

`type`: string 两个值 rhino 或者 frida 告诉用户这是什么脚本

`version`: string 版本号 例如 1.0.0

`url`: string 脚本的下载地址

`desc`: string 脚本描述，控制在30字以内，简单的描述，详细描述写到markdown中

`down_count`: int 脚本下载数量

## 完整格式

完整格式下仓库可以用于更多的功能

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

`name`: string 仓库名称

`icon`: string 仓库图标的url地址

`list`: string 列表格式的url地址

`push`: string 推送配置url地址

`markdown`: string 仓库详细说明markdown文件url地址

`group_qq`: string qq群的key 在这里获取 [https://qun.qq.com/join.html](https://qun.qq.com/join.html)

`group_tg`: string 例如群链接为 https://t.me/jshookgroup 填写jshookgroup即可

`user_count`: int 仓库用户数量

### 推送配置

如果仓库使用了完整格式，需要使用推送的话，push文件的json格式如下

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

jshook的设置中允许接收消息通知才能收到推送内容

为了不干扰用户，推送不会实时收到，有触发条件，当用户打开jshook或者其他注入jshook服务的应用时会开始拉取推送内容，通过id判断用户如果没有接收过开始消息通知

`id`: string 推送唯一标识

`title`: string 消息标题

`args`: string 当action为markdown时填写markdown文件url地址

`action`: string 跳转类型，固定值为markdown

## DeepLink

在html中可以使用以下方式跳转jshook添加仓库订阅，其实url为仓库的订阅url地址

```html
<a href="jshook://store?url=http://xxxxx.com">添加仓库订阅</>
```
