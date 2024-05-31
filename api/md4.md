# media

用于播放音乐

## media.create(data)

`参数`:

`data`: url地址或者文件base64值

`返回值`: 实例

调用后默认会自动播放，无需调用start

## [实例].start()

开始播放

## [实例].pause()

暂停播放

## [实例].stop()

停止播放

## [实例].loop(state)

`参数`:

`state`: boolean

是否循环播放，默认音乐只播放一次

## media.closeAll()

关闭所有实例
