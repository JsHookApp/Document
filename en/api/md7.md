# file

File operations.

## file.isFile(path)

`Parameters`:

`path`: string

`Returns`: boolean

## file.isDir(path)

`Parameters`:

`path`: string

`Returns`: boolean

## file.isExists(path)

`Parameters`:

`path`: string

`Returns`: boolean

## file.read(path)

`Parameters`:

`path`: string

`Returns`: string

## file.readBytes(path)

`Parameters`:

`path`: string

`Returns`: byte[]

## file.readliens(path,num)

Read file content by lines.

`Parameters`:

`path`: string — File path

`num`: long — Number of lines to read

`Returns`: List\<string\>

## file.write(path,content)

`Parameters`:

`path`: string

`content`: string

## file.writeBytes(path,content)

`Parameters`:

`path`: string

`content`: byte[]

## file.append(path,content)

`Parameters`:

`path`: string

`content`: string

## file.appendBytes(path,content)

`Parameters`:

`path`: string

`content`: byte[]

## file.copy(path,topath)

`Parameters`:

`path`: string

`topath`: string

## file.move(path,topath)

`Parameters`:

`path`: string

`topath`: string

## file.rename(path,newname)

`Parameters`:

`path`: string

`newname`: string

## file.delete(path)

`Parameters`:

`path`: string

## file.getName(path)

`Parameters`:

`path`: string

## file.getSize(path)

`Returns`: long

## file.zip(path,topath,passwd)

`Parameters`:

`path`: string

`topath`: string

`passwd`: string

## file.zip(path,topath)

`Parameters`:

`path`: string

`topath`: string

## file.unzip(path,topath,passwd)

`Parameters`:

`path`: string

`topath`: string

`passwd`: string

## file.unzip(path,topath)

`Parameters`:

`path`: string

`topath`: string
