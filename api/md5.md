# crypto

用于进行字符串加密解密

## crypto.encrypt(key,data,enctype,transformation)

`参数`:

`key`: string

`data`: string

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: 转换的名称 例如 `DES/CBC/PKCS5Padding`

`返回值`: string

## crypto.encryptBytes(key,data,enctype,transformation)

`参数`:

`key`: byte[]

`data`: byte[]

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: 转换的名称 例如 `DES/CBC/PKCS5Padding`

`返回值`: byte[]

## crypto.decrypt(key,data,enctype,transformation)

`参数`:

`key`: string

`data`: string

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: 转换的名称 例如 `DES/CBC/PKCS5Padding`

`返回值`: string

## crypto.decryptBytes(key,data,enctype,transformation)

`参数`:

`key`: byte[]

`data`: byte[]

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: 转换的名称 例如 `DES/CBC/PKCS5Padding`

`返回值`: byte[]

## crypto.rc4Encrypt(key,data)

`参数`:

`key`: string

`data`: string

`返回值`: string

## crypto.rc4EncryptBytes(key,data)

`参数`:

`key`: byte[]

`data`: byte[]

`返回值`: byte[]

## crypto.rc4Decrypt(key,data)

`参数`:

`key`: string

`data`: string

`返回值`: string

## crypto.rc4DecryptBytes(key,data)

`参数`:

`key`: byte[]

`data`: byte[]

`返回值`: byte[]

## crypto.md5(data)

`参数`:

`data`: string

`返回值`: string

## crypto.md5Bytes(data)

`参数`:

`data`: byte[]

`返回值`: string

## crypto.sha1(data)

`参数`:

`data`: string

`返回值`: string

## crypto.sha1Bytes(data)

`参数`:

`data`: byte[]

`返回值`: string

## crypto.sha256(data)

`参数`:

`data`: string

`返回值`: string

## crypto.sha256Bytes(data)

`参数`:

`data`: byte[]

`返回值`: string
