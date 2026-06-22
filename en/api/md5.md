# crypto

Encrypt, decrypt, and hash strings and byte arrays (AES, DES, RC4, MD5, SHA-1, SHA-256).

## crypto.encrypt(key,data,enctype,transformation)

`Parameters`:

`key`: string

`data`: string

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: Transformation name, e.g., `DES/CBC/PKCS5Padding`

`Returns`: string

## crypto.encryptBytes(key,data,enctype,transformation)

`Parameters`:

`key`: byte[]

`data`: byte[]

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: Transformation name, e.g., `DES/CBC/PKCS5Padding`

`Returns`: byte[]

## crypto.decrypt(key,data,enctype,transformation)

`Parameters`:

`key`: string

`data`: string

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: Transformation name, e.g., `DES/CBC/PKCS5Padding`

`Returns`: string

## crypto.decryptBytes(key,data,enctype,transformation)

`Parameters`:

`key`: byte[]

`data`: byte[]

`enctype`: CRYPTO_AES | CRYPTO_DES

`transformation`: Transformation name, e.g., `DES/CBC/PKCS5Padding`

`Returns`: byte[]

## crypto.rc4Encrypt(key,data)

`Parameters`:

`key`: string

`data`: string

`Returns`: string

## crypto.rc4EncryptBytes(key,data)

`Parameters`:

`key`: byte[]

`data`: byte[]

`Returns`: byte[]

## crypto.rc4Decrypt(key,data)

`Parameters`:

`key`: string

`data`: string

`Returns`: string

## crypto.rc4DecryptBytes(key,data)

`Parameters`:

`key`: byte[]

`data`: byte[]

`Returns`: byte[]

## crypto.md5(data)

`Parameters`:

`data`: string

`Returns`: string

## crypto.md5Bytes(data)

`Parameters`:

`data`: byte[]

`Returns`: string

## crypto.sha1(data)

`Parameters`:

`data`: string

`Returns`: string

## crypto.sha1Bytes(data)

`Parameters`:

`data`: byte[]

`Returns`: string

## crypto.sha256(data)

`Parameters`:

`data`: string

`Returns`: string

## crypto.sha256Bytes(data)

`Parameters`:

`data`: byte[]

`Returns`: string
