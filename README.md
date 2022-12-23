# HaLo chip

An easy to use javascript library for interacting with HaLo chips

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
console.log('data', signature)
```

## API


### <a name="listkeys"></a>listkeys() ⇒ <code>keys</code>
List the keys of the device

#### Returns
* `object[]` - The list of keys
    * `object[].key` - The public key
    * `object[].slot` - Slot number of the key
    * `object[].address` - Ethereum address of the key
    * `object[].did` - PKH DID of the key



### <a name="ethsignmessage"></a>ethSignMessage(message, slot, address) ⇒ <code>signature</code>
Sign a message using EIP191.

#### Params
* `message`: `string` - The message to sign
* `slot`: `number` - The slot index of the key to use
* `address`: `string` - The the ethereum address of the key used

#### Returns
* `string` - The signature encoded as a hex string



### <a name="ethsignhash"></a>ethSignHash(hash, slot, address) ⇒ <code>signature</code>
Sign a hash and return a recoverable signature.

#### Params
* `hash`: `string` - The hex encoded hash to sign
* `slot`: `number` - The slot index of the key to use
* `address`: `string` - The the ethereum address of the key used

#### Returns
* `string` - The signature encoded as a hex string



### <a name="sign"></a>sign(hash, slot) ⇒ <code>signature</code>
Sign a hash

#### Params
* `hash`: `string` - The hex encoded hash to sign
* `slot`: `number` - The slot index of the key to use

#### Returns
* `object` - The signature
    * `object.r` - The r value encoded as hex
    * `object.s` - The s value encoded as hex



### <a name="generatekey"></a>generateKey() ⇒ <code>void</code>
Generate the 3rd key of the Halo chip.



### <a name="writestorage"></a>writeStorage(slot, data) ⇒ <code>void</code>
Write a 32 bytes to the latch storage.
Warning: writing to the storage is permanent, not possible
to remove or update the value afterwards.

#### Params
* `slot`: `number` - The slot index of the key to use
* `data`: `string` - The 32 bytes encoded as a hex string



### <a name="readstorage"></a>readStorage(slot) ⇒ <code>data</code>
Read the 32 bytes from the latch storage.

#### Params
* `slot`: `number` - The slot index of the key to use

#### Returns
* `string` - The data in the storage slot

## License
MIT
