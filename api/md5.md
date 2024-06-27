# crypto

Used for string encryption and decryption

## crypto.encrypt(key,data,enctype,transformation)

`Parameters`:

`key`: string

`data`: string

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: name of the transformation, for example `DES/CBC/PKCS5Padding`

`Return value`: string

## crypto.encryptBytes(key,data,enctype,transformation)

`Parameters`:

`key`: byte[]

`data`: byte[]

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: name of the transformation, for example `DES/CBC/PKCS5Padding`

`Return value`: byte[]

## crypto.decrypt(key,data,enctype,transformation)

`Parameters`:

`key`: string

`data`: string

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: name of the transformation e.g. `DES/CBC/PKCS5Padding`

`return`: string

## crypto.decryptBytes(key,data,enctype,transformation)

`parameters`:

`key`: byte[]

`data`: byte[]

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: name of the transformation e.g. `DES/CBC/PKCS5Padding`

`return`: byte[]

## crypto.rc4Encrypt(key,data)

`parameters`:

`key`: string

`data`: string

`return`: string

## crypto.rc4EncryptBytes(key,data)

`parameters`:

`key`: byte[]

`data`: byte[]

`return`: byte[]

## crypto.rc4Decrypt(key,data)

`parameters`:

`key`: string

`data`: string

`return`: string

## crypto.rc4DecryptBytes(key,data)

`parameters`:

`key`: byte[]

`data`: byte[]

`return`: byte[]

## crypto.md5(data)

`parameters`:

`data`: string

`return`: string

## crypto.md5Bytes(data)

`parameters`:

`data`: byte[]

`return`: string

## crypto.sha1(data)

`parameters`:

`data`: string

`return`: string

## crypto.sha1Bytes(data)

`Parameters`:

`data`: byte[]

`Return value`: string

## crypto.sha256(data)

`Parameters`:

`data`: string

`Return value`: string

## crypto.sha256Bytes(data)

`Parameters`:

`data`: byte[]

`Return value`: string
