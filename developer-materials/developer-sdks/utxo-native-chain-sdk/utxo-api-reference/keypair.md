# Keypair



#### createKeypair[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#createkeypair) <a href="#createkeypair" id="createkeypair"></a>

_**- Creates an instance of `WalletKeypar` using password.**_\
This method is used to restore a wallet keypair. The Keypair contains some essential information, such as:

* &#x20; address
* &#x20; public key
* &#x20; key store

and so on, and it is used for pretty much any personalized operation that user can do using FindoraSdk

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#parameters)

* &#x20; `<string>` - Password to be used to generate an encrypted KeyStore

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#results)

* &#x20; `Promise<WalletKeypar>` - An instance of `WalletKeypar`

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#example)

```typescript
const password = "qsjEI%123";

// Create a wallet info object using given password
const walletPair = await Keypair.createKeypair(password);
```

#### getAddressByPublicKey[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#getaddressbypublickey) <a href="#getaddressbypublickey" id="getaddressbypublickey"></a>

_**- Get wallet address by given public key**_\
Using this function user can retreive the wallet address by given public key

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#parameters-1)

* &#x20; `<string>` - Public key

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#results-1)

* &#x20; `Promise<string>` - A wallet address.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#example-1)

```typescript
const pubkey = "qsjEI%123";
// Get wallet address by public key
const walletAddress = await Keypair.getAddressByPublicKey(pubkey);
```

#### getAddressPublicAndKey[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#getaddresspublicandkey) <a href="#getaddresspublicandkey" id="getaddresspublicandkey"></a>

_**- Create an instance of `LightWalletKeypair` using given wallet address.**_\
This method is used to create a light version of the WalletKeypar using given wallet address.The LightWalletKeypair contains two essential information:

* &#x20; address
* &#x20; public key

It's a light version of the WalletKeypar, containing only address and publickey

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#parameters-2)

* &#x20; `<string>` - Wallet address

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#results-2)

* &#x20; `Promise<LightWalletKeypair>` - An instance of `LightWalletKeypair`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#example-2)

```typescript
const address = "fra234xfde4";

// Create a LightWalletKeypair object using given address
const lightWalletKeypair = await Keypair.getAddressPublicAndKey(address);
```

#### getMnemonic[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#getmnemonic) <a href="#getmnemonic" id="getmnemonic"></a>

_**- Creates an array of Mnemonic phrases.**_\
This method is used to creates an array of Mnemonic phrases.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#parameters-3)

* &#x20; `<number>` - Desired length of mnemonic phrases. It can only be 12/15/18/21/24.
* &#x20; `<string>` - (optional) Default is `en`.

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#results-3)

* &#x20; `Promise<LightWalletKeypair>` - An instance of `LightWalletKeypair`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#example-3)

```typescript
const desiredLength = 24;

// Create a wallet info object using given password
const mnemonic = await Keypair.getMnemonic(desiredLength);
```

#### restoreFromMnemonic[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#restorefrommnemonic) <a href="#restorefrommnemonic" id="restorefrommnemonic"></a>

_**- Creates an instance of `WalletKeypar` using Mnemonic and password.**_\
This method is used to restore a wallet keypair. The Keypair contains some essential information, such as:

* &#x20; address
* &#x20; public key
* &#x20; key store

and so on, and it is used for pretty much any personalized operation that user can do using FindoraSdk

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#parameters-4)

* &#x20; `<string[]>` - mnemonic words
* &#x20; `<string>` - Password to be used to generate an encrypted KeyStore

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#results-4)

* &#x20; `Promise<WalletKeypar>` - An instance of `WalletKeypar`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#example-4)

```typescript
const password = "qsjEI%123";
const mnemonic = ["Apple", "Orange", "Banana"];

// Create a wallet info object using given Mnemonic and password
const walletPair = await Keypair.restoreFromMnemonic(mnemonic, password);
```

#### restoreFromPrivateKey[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#restorefromprivatekey) <a href="#restorefromprivatekey" id="restorefromprivatekey"></a>

_**- Creates an instance of `WalletKeypar` using given private key and password.**_\
This method is used to restore a wallet keypair. The Keypair contains some essential information, such as:

* &#x20; address
* &#x20; public key
* &#x20; key store

and so on, and it is used for pretty much any personalized operation that user can do using FindoraSdk

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#parameters-5)

* &#x20; `<string>` - Private key
* &#x20; `<string>` - Password to be used to generate an encrypted KeyStore

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#results-5)

* &#x20; `Promise<WalletKeypar>` - An instance of `WalletKeypar`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_keypair#example-5)

```typescript
const password = "qsjEI%123";
const pkey = "XXXXXXXXXX";

// Create a wallet info object using given private key and password
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);
```
