# Transaction

#### getTransactionBuilder[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#gettransactionbuilder) <a href="#gettransactionbuilder" id="gettransactionbuilder"></a>

_**- Create an instance of `TransactionBuilder`**_\
This method is used to create a transaction builder

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#results)

* &#x20; `Promise<TransactionBuilder>` - TransactionBuilder which should be used in `Transaction.submitTransaction`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#example)

```typescript
// Create a TransactionBuilder object
const transactionBuilder = await Transaction.getTransactionBuilder();
```

#### getTxList[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#gettxlist) <a href="#gettxlist" id="gettxlist"></a>

_**- Get a list of transactions for given wallet address**_\
This method is used to get a list of transactions for given wallet address

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#parameters)

* &#x20; `<string>` - wallet address
* &#x20; `<"to" | "from">` - transaction type. it can only be 'to' or 'from'
* &#x20; `<number>` - pagination. The defaul value is 1.

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#results-1)

* &#x20; `Promise<ProcessedTxListResponseResult>` - An instance of `ProcessedTxListResponseResult` containing the total count and transactions.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#example-1)

```typescript
const address = `fra000xxsr`;
const type = "to";

// Get list of `to` transaction of given address
const txDetail = await Transaction.getTxList(address, type);
```

#### sendToAddress[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#sendtoaddress) <a href="#sendtoaddress" id="sendtoaddress"></a>

_**- Send some asset to an address**_\
Using this function, user can transfer some amount of given asset to another address

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#parameters-1)

* &#x20; `<WalletKeypar>` - wallet keypair
* &#x20; `<string>` - target wallet address
* &#x20; `<string>` - amount to be sent
* &#x20; `<string>` - asset code
* &#x20; `<AssetBlindRules>` - (optional) confidential options for blind rule

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#results-2)

* &#x20; `Promise<TransactionBuilder>` - A TransactionBuilder which should be used in Transaction.submitTransaction

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#example-2)

```typescript
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);
const toWalletInfo = await Keypair.restoreFromPrivateKey(toPkeyMine2, password);

const assetCode = await Asset.getFraAssetCode();

const assetBlindRules: Asset.AssetBlindRules = {
  isTypeBlind: false,
  isAmountBlind: false,
};

const transactionBuilder = await Transaction.sendToAddress(
  walletInfo,
  toWalletInfo.address,
  "2",
  assetCode,
  assetBlindRules
);

const resultHandle = await Transaction.submitTransaction(transactionBuilder);
```

#### sendToMany[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#sendtomany) <a href="#sendtomany" id="sendtomany"></a>

_**- Send some asset to multiple receivers**_\
Using this function, user can transfer perform multiple transfers of the same asset to multiple receivers using different amounts

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#parameters-2)

* &#x20; `<WalletKeypar>` - wallet keypair
* &#x20; `<TransferReciever[]>` - the list of target wallet addresses and amount
* &#x20; `<string>` - asset code
* &#x20; `<AssetBlindRules>` - (optional) confidential options for blind rule

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#results-3)

* &#x20; `Promise<TransactionBuilder>` - A TransactionBuilder which should be used in Transaction.submitTransaction

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#example-3)

```typescript
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);
const toWalletInfoMine2 = await Keypair.restoreFromPrivateKey(
  toPkeyMine2,
  password
);
const toWalletInfoMine3 = await Keypair.restoreFromPrivateKey(
  toPkeyMine3,
  password
);

const assetCode = await Asset.getFraAssetCode();

const assetBlindRules: Asset.AssetBlindRules = {
  isTypeBlind: false,
  isAmountBlind: false,
};

const recieversInfo = [
  { reciverWalletInfo: toWalletInfoMine2, amount: "2" },
  { reciverWalletInfo: toWalletInfoMine3, amount: "3" },
];

const transactionBuilder = await Transaction.sendToMany(
  walletInfo,
  recieversInfo,
  assetCode,
  assetBlindRules
);

const resultHandle = await Transaction.submitTransaction(transactionBuilder);
```

#### sendToPublicKey[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#sendtopublickey) <a href="#sendtopublickey" id="sendtopublickey"></a>

_**- Send some asset to a wallet by public key**_\
Using this function, user can transfer some amount of given asset to another wallet by target's public key

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#parameters-3)

* &#x20; `<WalletKeypar>` - wallet keypair
* &#x20; `<string>` - target's public key
* &#x20; `<string>` - amount to be sent
* &#x20; `<string>` - asset code
* &#x20; `<AssetBlindRules>` - (optional) confidential options for blind rule

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#results-4)

* &#x20; `Promise<TransactionBuilder>` - A TransactionBuilder which should be used in Transaction.submitTransaction

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#example-4)

```typescript
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);
const toWalletPublicKey = `tgshauuy213`;

const assetCode = await Asset.getFraAssetCode();

const assetBlindRules: Asset.AssetBlindRules = {
  isTypeBlind: false,
  isAmountBlind: false,
};

const transactionBuilder = await Transaction.sendToPublicKey(
  walletInfo,
  toWalletPublicKey,
  "2",
  assetCode,
  assetBlindRules
);

const resultHandle = await Transaction.submitTransaction(transactionBuilder);
```

#### submitTransaction[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#submittransaction) <a href="#submittransaction" id="submittransaction"></a>

_**- Submits a transaction**_\
The next step after creating a transaction is submitting it to the ledger, and, as a response, we retrieve the transaction handle.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#parameters-4)

* &#x20; `<TransactionBuilder>` - an instance of `TransactionBuilder`

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#results-5)

* &#x20; `Promise<string>` - Transaction status handle

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_transaction#example-5)

```typescript
onst walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

// First, we create a transaction builder
const assetBuilder = await Asset.defineAsset(walletInfo, assetCode);

// Then, we submit a transaction
// If succcesful, the response of the submit transaction request will return a handle that can be used the query the status of the transaction.
const handle = await Transaction.submitTransaction(assetBuilder);
```
