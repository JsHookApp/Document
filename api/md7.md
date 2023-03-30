# file

用于对文件进行相关操作

## file.isFile(path)

`参数`:

`path`: string

`返回值`: boolean

## file.isDir(path)

`参数`:

`path`: string

`返回值`: boolean

## file.isExists(path)

`参数`:

`path`: string

`返回值`: boolean

## file.read(path)

`参数`:

`path`: string

`返回值`: string

## file.readBytes(path)

`参数`:

`path`: string

`返回值`: byte[]

## file.write(path,content)

`参数`:

`path`: string

`content`: string

## file.writeBytes(path,content)

`参数`:

`path`: string

`content`: byte[]

## file.append(path,content)

`参数`:

`path`: string

`content`: string

## file.appendBytes(path,content)

`参数`:

`path`: string

`content`: byte[]

## file.copy(path,topath)

`参数`:

`path`: string

`topath`: string

## file.move(path,topath)

`参数`:

`path`: string

`topath`: string

## file.rename(path,newname)

`参数`:

`path`: string

`newname`: string

## file.delete(path)

`参数`:

`path`: string

## file.getName(path)

`参数`:

`path`: string

## file.getSize(path)

`返回值`: long

## file.zip(path,topath,passwd)

`参数`:

`path`: string

`topath`: string

`passwd`: string

## file.zip(path,topath)

`参数`:

`path`: string

`topath`: string

## file.unzip(path,topath,passwd)

`参数`:

`path`: string

`topath`: string

`passwd`: string

## file.unzip(path,topath)

`参数`:

`path`: string

`topath`: string
