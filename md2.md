# 自建仓库

需要搭建属于自己的脚本仓库，只需要提供以下格式的json文件地址即可，仓库界面右上角菜单中配置地址

```json
[
    {
        "author": "作者名称",
        "markdown": "markdown的地址",
        "ctime": "生成时间(0000-00-00)",
        "source": "脚本来源地址",
        "id": "脚本唯一标识(推荐uuid)",
        "title": "脚本名称",
        "type": "脚本类型(rhino/frida)",
        "version": "版本号",
        "url": "脚本下载地址",
        "desc": "脚本描述"
    }
]
```