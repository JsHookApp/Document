# Custom Repository

To set up your own script repository, you only need to provide a JSON file URL in the specified format. Configure the URL in the repository page's top-right menu. `Fields that are not needed can be null or omitted.`

## List Format

With the list format, the repository only shows the script list. For more features, refer to the full format below.

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

Field descriptions:

`author`: string — Script author name

`markdown`: string — URL to detailed markdown documentation

`ctime`: string — Script creation date, format: YYYY-MM-DD

`source`: string — Source URL (e.g., GitHub repo), not the download URL

`id`: string — Unique script identifier, can use UUID

`title`: string — Script name

`type`: string — Either `rhino` or `frida` to indicate the script type

`version`: string — Version number, e.g., 1.0.0

`url`: string — Script download URL

`desc`: string — Short description (under 30 characters), detailed description goes in markdown

`down_count`: int — Script download count

## Full Format

The full format enables additional features for the repository.

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

`name`: string — Repository name

`icon`: string — Repository icon URL

`list`: string — URL to the list format JSON

`push`: string — Push notification config URL

`markdown`: string — Repository markdown documentation URL

`group_qq`: string — QQ group key, get it from [https://qun.qq.com/join.html](https://qun.qq.com/join.html)

`group_tg`: string — Telegram group name, e.g., for https://t.me/jshookgroup enter `jshookgroup`

`user_count`: int — Repository user count

### Push Notifications

If the repository uses the full format and needs push notifications, the push JSON format is:

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

Push notifications are only delivered if the user has allowed message notifications in JsHook's settings.

To avoid disturbing users, pushes are not delivered in real time — they are triggered on demand. When the user opens JsHook, or opens any other app into which the JsHook service is injected, the client pulls the latest push content. The `id` field is used to determine whether the user has already received a given notification.

`id`: string — Unique push identifier

`title`: string — Notification title

`args`: string — When `action` is `markdown`, the URL of the markdown file to open

`action`: string — Navigation type; the only supported value is `markdown`

## DeepLink

In HTML, you can use the following link to prompt JsHook to add a repository subscription. The `url` parameter is the repository's subscription URL.

```html
<a href="jshook://store?url=http://xxxxx.com">Add repository subscription</a>
```
