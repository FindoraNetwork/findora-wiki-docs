# Asset



#### defineAsset[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#defineasset) <a href="#defineasset" id="defineasset"></a>

_**- Defines a custom asset**_\
An asset definition operation registers an asset with the Findora ledger. An asset is a digital resource that can be issued and transferred.\
An asset has an issuer and a unique code. The DefineAsset operation must provide an unused token code. The transaction containing the DefineAsset operation will fail if there is already another asset on the ledger with the same code.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#parameters)

* &#x20; `<WalletKeypar>` - Wallet keypair
* &#x20; `<string>` - asset name
* &#x20; `<string>` - (optinal) asset memo
* &#x20; `<string>` - (optinal) A set of rules (options) for the new asset.

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#results)

* &#x20; `Promise<TransactionBuilder>` - An instance of `TransactionBuilder` from `Ledger`

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#example)

```typescript
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

// First, we create a transaction builder
const assetBuilder = await Asset.defineAsset(walletInfo, assetCode);

// Then, we submit a transaction
const handle = await Transaction.submitTransaction(assetBuilder);
```

#### getAssetCode[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#getassetcode) <a href="#getassetcode" id="getassetcode"></a>

_**- Return Asset Code**_\
This method returns Asset Code by given asset type

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#parameters-1)

* &#x20; `<number[]>` - asset type

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#results-1)

* &#x20; `Promise<string>` - asset code.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#example-1)

```typescript
const assetType = [1, 2];

// Get the decrypted Asset code
const assetCode = await Asset.getAssetCode(assetType);
```

#### getAssetDetails[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#getassetdetails) <a href="#getassetdetails" id="getassetdetails"></a>

_**- Get Asset Details**_\
This method returns Asset details by given asset code

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#parameters-2)

* &#x20; `<string>` - asset code

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#results-2)

* &#x20; `Promise<IAsset>` - An instance of `FindoraWallet.IAsset`

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#example-2)

```typescript
const assetCode = "Your_Asset_Code";

// Get asset details
const assetDetails = await getAssetDetails(assetCode);
```

#### getFraAssetCode[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#getfraassetcode) <a href="#getfraassetcode" id="getfraassetcode"></a>

_**- Returns the pre-defined FRA asset code**_\
FRA asset code can not be re-defined, as well as it can not be used in the `DefineAset` or `IssueAsset` operations.\
This is the main asset code, which is used when user needs to create a transaction, or calculate the fee and so on.

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#results-3)

* &#x20; `Promise<string>` - Findora Asset code

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#example-3)

```typescript
// Get the FRA Asset code
const fraAssetCode = await Asset.getFraAssetCode();
```

#### getFraPublicKey[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#getfrapublickey) <a href="#getfrapublickey" id="getfrapublickey"></a>

_**- Return Destination's Public Key**_\
This method returns the public key of destination

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#results-4)

* &#x20; `Promise<XfrPublicKey>` - An instance of `XfrPublicKey`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#example-4)

```typescript
// Get the public key of destination
const pubKey = await Asset.getFraPublicKey();
```

#### getMinimalFee[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#getminimalfee) <a href="#getminimalfee" id="getminimalfee"></a>

_**- Return Minimal Fee for transaction**_\
This method returns the required minimal fee for transaction

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#results-5)

* &#x20; `Promise<BigInt>` - An instance of `BigInt`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#example-5)

```typescript
// Get the minimal fee for transaction
const minFee = await Asset.getMinimalFee();
```

#### getRandomAssetCode[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#getrandomassetcode) <a href="#getrandomassetcode" id="getrandomassetcode"></a>

_**- Returns a random asset code**_\
Using `Ledger`, it generates and returns a random custom asset code

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#results-6)

* &#x20; `Promise<string>` - Asset code.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#example-6)

```typescript
// Get a random asset code
const assetCode = await Asset.getRandomAssetCode();
```

#### issueAsset[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#issueasset) <a href="#issueasset" id="issueasset"></a>

_**- Issue some amount of a custom asset**_\
Asset issuers can use the `IssueAsset` operation to mint units of an asset that they have created. Concretely, the `IssueAsset` operation creates asset records that represent ownership by a public key of a certain amount of an asset. These asset records are stored in a structure called a transaction output (TXO).

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#parameters-3)

* &#x20; `<WalletKeypar>` - wallet keypair
* &#x20; `<string>` - asset name
* &#x20; `<string>` - amount to be issued
* &#x20; `<AssetBlindRules>` - asset blind rules
* &#x20; `<number>` - (optional) asset decimals. This parameter can define how many numbers after the comma would this asset have

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#results-7)

* &#x20; `Promise<TransactionBuilder>` - An instance of `TransactionBuilder` from `Ledger`

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_asset#example-7)

```typescript
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

// Define the new asset parameters (rules)
const assetBlindRules = { isAmountBlind: false };

// First, we create a transaction builder
const assetBuilder = await Asset.issueAsset(
  walletInfo,
  customAssetCode,
  amountToIssue,
  assetBlindRules
);

// Then, we submit a transaction
const handle = await Transaction.submitTransaction(assetBuilder);tyty
```
