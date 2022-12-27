# HaLo chip

An easy to use javascript library for interacting with [HaLo chips](https://medium.com/kong-land-embassy/eternal-physical-crypto-b487ee8a1553)

## Installation

    npm i halo-chip

## Usage

```javascript
import { listKeys, ethSignMessage } from `halo-chip`

const keys = await listKeys()
console.log('keys:')
keys.map(k => console.log)
const address = keys[0].address

const signature = await ethSignMessage('test123', 1, address)
console.log('signature:', signature)
```

## API


### `listkeys()` ⇒ `keys`
List the keys of the device

#### Returns
* `object[]` - The list of keys
    * `object[].key` - The public key
    * `object[].slot` - Slot number of the key
    * `object[].address` - Ethereum address of the key
    * `object[].did` - PKH DID of the key



### `ethSignMessage(message, slot, address)` ⇒ `signature`
Sign a message using EIP191.

#### Params
* `message`: `string` - The message to sign
* `slot`: `number` - The slot index of the key to use
* `address`: `string` - The the ethereum address of the key used

#### Returns
* `string` - The signature encoded as a hex string



### `ethSignHash(hash, slot, address)` ⇒ `signature`
Sign a hash and return a recoverable signature.

#### Params
* `hash`: `string` - The hex encoded hash to sign
* `slot`: `number` - The slot index of the key to use
* `address`: `string` - The the ethereum address of the key used

#### Returns
* `string` - The signature encoded as a hex string



### `sign(hash, slot)` ⇒ `signature`
Sign a hash

#### Params
* `hash`: `string` - The hex encoded hash to sign
* `slot`: `number` - The slot index of the key to use

#### Returns
* `object` - The signature
    * `object.r` - The r value encoded as hex
    * `object.s` - The s value encoded as hex



### `generateKey()` ⇒ `void`
Generate the 3rd key of the Halo chip.


### `writeStorage(slot, data)` ⇒ `void`
Write a 32 bytes to the latch storage.

> ***Warning:***
> Write operation is permanent. It's not possible
to remove or update the value afterwards.

#### Params
* `slot`: `number` - The slot index of the key to use
* `data`: `string` - The 32 bytes encoded as a hex string



### `readStorage(slot)` ⇒ `data`
Read the 32 bytes from the latch storage.

#### Params
* `slot`: `number` - The slot index of the key to use

#### Returns
* `string` - The data in the storage slot

## License
MIT
