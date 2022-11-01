# Account



#### create[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#create) <a href="#create" id="create"></a>

_**- Creates an instance of WalletKeypar using password.**_\
This method is used to create a WalletKeypar using password. The Keypair contains some essential information, such as:

* &#x20; address
* &#x20; public key
* &#x20; key store

and so on, and it is used for pretty much any personalized operation that user can do using FindoraSdk

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#parameters)

* &#x20; `<string>` - Password of account

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#results)

* &#x20; `Promise<WalletKeypar>` - An instance of `WalletKeypar`

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#example)

{% code overflow="wrap" %}
```typescript
const password = "qsjEI%123";

// Create a wallet info object using given password
const walletInfo = await Account.create(password);
```
{% endcode %}

#### getBalance[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#getbalance) <a href="#getbalance" id="getbalance"></a>

_**- Get the balance of the specific asset for the given user**_

Using this function user can retrieve the balance for the specific asset code, which could be either custom asset or an FRA asset

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#parameters-1)

* &#x20; `<WalletKeypar>` - An instance of WalletKeypar
* &#x20; `<string>` - (optional) Asset Code which could be either custom asset or an FRA asset.

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#results-1)

* &#x20; `Promise<string>` - The balance of the specific asset for the given user.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#example-1)

```typescript
const pkey = "lfyd1234!";
const password = "uuicnf!34";

// Restore Wallet
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

// Get balance
const balance = await Account.getBalance(walletInfo, customAssetCode);
```

#### getBalanceInWei[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#getbalanceinwei) <a href="#getbalanceinwei" id="getbalanceinwei"></a>

_**- Get the balance of the specific asset for the given user in Wei format**_

Using this function user can retrieve the balance for the specific asset code, which could be either custom asset or an FRA asset

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#parameters-2)

* &#x20; `<WalletKeypar>` - An instance of WalletKeypar
* &#x20; `<string>` - (optional) Asset Code which could be either custom asset or an FRA asset.

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#results-2)

* &#x20; `Promise<BigNumberValue>` - The balance of the specific asset for the given user in Wei format.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#example-2)

```typescript
const pkey = "lfyd1234!";
const password = "uuicnf!34";

// Restore Wallet
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

// Get balance in Wei format
const balance = await Account.getBalanceInWei(walletInfo, customAssetCode);
```

#### getCreatedAssets[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#getcreatedassets) <a href="#getcreatedassets" id="getcreatedassets"></a>

_**- Get an array of instances of ProcessedIssuedRecord using wallet address.**_

This method is used to get created Assets. The ProcessedIssuedRecord contains some essential information, such as:

* &#x20; code
* &#x20; record
* &#x20; id
* &#x20; ownerMemo

and so on. It's the issued asset.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#parameters-3)

* &#x20; `<string>` - Wallet address.

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#results-3)

* &#x20; `Promise<ProcessedIssuedRecord[]>` - an array of `ProcessedIssuedRecord` instances.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_account#example-3)

```typescript
const pkey = "lfyd1234!";
const password = "uuicnf!34";

// Restore Wallet
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

// Get balance in Wei format
const balance = await Account.getBalanceInWei(walletInfo, customAssetCode);
```
