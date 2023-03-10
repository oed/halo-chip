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

### Usage with Ceramic

```javascript
import { DIDSession } from 'did-session'
import { EthereumWebAuth, getAccountId } from '@didtools/pkh-ethereum'

const keys = await listKeys()
const { address, slot } = keys[0]
const accountId = { address: address.toLowerCase(), chainId: { reference: 1, namespace: 'eip155' } }
  
const authMethod = await EthereumWebAuth.getAuthMethod({
  request: async ({ method, params }) => ethSignMessage(params[0], slot, params[1])
}, accountId)
const session = await DIDSession.authorize(authMethod, { resources: ['ceramic://*?model=kjz...'] })
```

### Parse url params
```javascript
import { parseURLParams } from `halo-chip`
const params = `?v=c3&static=4104FAC52DEA1D02FC0F1473B832B88F15DC9CEFBFEE690C3C9B8FECF8045B2A06166119F5C539E9FF418A58DA95ED057DB17E76E9B57531025BEFE4B45EB0DF07634104422738D17192382F19482649E07022615930C3C1CB29A51CFE23D62445CDB8729A40DE69A79697F3704C7D684365846CF6DB974E33E47998BDB2DAB1131D330E000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000&latch1=E5D961F8DAD5F030F57E88E72AAD26492D722AFB5CC84256DCA2BA6362BEBF51&latch2=0000000000000000000000000000000000000000000000000000000000000000&cmd=81020000001B8F48E0B1A3B19C5DF8D763717A7BE27475FA6AF0E34F8449704C3A8B00&res=3046022100D5871CDE09C5AB891F4D023EC278DF8F1CE5B6970F478C825D812C946F15593B022100EA326B2683E212F34CF87C051CF0BA00BCD1530B72FE8D8754584F480C38ED3400000000`
const parsed = parseURLParams(params)
console.log(parsed)
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


### `parseURLParams(params)` => `parsed`
Parse the url parameters generated when scanning a HaLo chip.

#### Params
* `params`: `string` - The query params to parse

#### Returns
* `object` - The parsed values
    * `object.tagVersion` - The version of the scanned chip
    * `object.keys[]` - The list of the keys
        * `object.keys[].key` - The public key
        * `object.keys[].slot` - Slot number of the key
        * `object.keys[].address` - Ethereum address of the key
        * `object.keys[].did` - PKH DID of the key
    * `object.proof` - The proof generated by the chip
        * `object.proof.challenge` - The 32 byte value signed in the proof (counter + random value)
        * `object.proof.signature` - The signature produced by the key at slot 2
        * `object.proof.counter` - The current value of the counter
    * `object.storage[]` - The list of values in the device storage
        * `object.keys[].value` - The value of this storage slot
        * `object.keys[].slot` - Slot number of this storage slot


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
