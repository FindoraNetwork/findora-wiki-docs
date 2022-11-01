# Staking

#### claim[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#claim) <a href="#claim" id="claim"></a>

_**- Claim FRA Token Rewards**_\
This function enables users to claim rewards earned from staking FRA tokens.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#parameters)

* &#x20; `<WalletKeypar>` - Wallet keypair
* &#x20; `<string>` - the amout of rewards which users wants to claim

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#results)

* &#x20; `Promise<TransactionBuilder>` - TransactionBuilder which should be used in `Transaction.submitTransaction`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#example)

```typescript
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

// First, we create a transaction builder
const assetBuilder = await Asset.defineAsset(walletInfo, assetCode);

// Then, we submit a transaction
const handle = await Transaction.submitTransaction(assetBuilder);
```

#### delegate[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#delegate) <a href="#delegate" id="delegate"></a>

_**- Delegates FRA tokens**_\
This function allows users to delegate FRA tokens to a validator.\
This functionality is nearly identical to Transaction.sendToAddress except it adds one additional operation (i.e. add\_operation\_delegate) to the transaction builder.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#parameters-1)

* &#x20; `<WalletKeypar>` - Wallet keypair
* &#x20; `<string>` - Target address for delegation
* &#x20; `<string>` - delegation amout
* &#x20; `<string>` - Asset Code
* &#x20; `<string>` - Target validator Address
* &#x20; `<AssetBlindRules>` - (optional) Confidential options for blind rule

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#results-1)

* &#x20; `Promise<TransactionBuilder>` - TransactionBuilder which should be used in `Transaction.submitTransaction`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#example-1)

```typescript
const ledger = await getLedger();

// This is the address funds are sent to.
// Actual `transfer to validator` process would be handled via added `add_operation_delegate` operation

const delegationTargetPublicKey = Ledger.get_delegation_target_address();
const delegationTargetAddress = await Keypair.getAddressByPublicKey(
  delegationTargetPublicKey
);

const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

const assetCode = await Asset.getFraAssetCode();

const assetBlindRules: Asset.AssetBlindRules = {
  isTypeBlind: false,
  isAmountBlind: false,
};

const transactionBuilder = await StakingApi.delegate(
  walletInfo,
  delegationTargetAddress,
  amount,
  assetCode,
  validatorAddress,
  assetBlindRules
);

const resultHandle = await Transaction.submitTransaction(transactionBuilder);
```

#### getDelegateInfo[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#getdelegateinfo) <a href="#getdelegateinfo" id="getdelegateinfo"></a>

_**- Get the delegation information**_\
This method is used to get the delegation information

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#parameters-2)

* &#x20; `<string>` - wallet address

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#results-2)

* &#x20; `Promise<DelegateInfoResponse>` - An instance of `DelegateInfoDataResult` containing the response and error..

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#example-2)

```typescript
const address = "fra123sxde";

// Get the delegation information
const delegateInfo = await StakingApi.getDelegateInfo(address);
```

#### getValidatorList[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#getvalidatorlist) <a href="#getvalidatorlist" id="getvalidatorlist"></a>

_**- Get validator list**_\
This method is used to get the list of validators.

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#results-3)

* &#x20; `Promise<validatorListResponse>` - An instance of `validatorListResponse` containing the response and error..

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#example-3)

```typescript
// Get validator list
const validatorList = await StakingApi.getValidatorList();
```

#### unStake[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#unstake) <a href="#unstake" id="unstake"></a>

_**- Unstake FRA tokens**_\
This function allows users to unstake (aka unbond) FRA tokens.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#parameters-3)

* &#x20; `<WalletKeypar>` - Wallet keypair
* &#x20; `<string>` - the amount users wants to unstake
* &#x20; `<string>` - validator's address
* &#x20; `<boolean>` - fully unstake option. Default is `false`

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#results-4)

* &#x20; `Promise<TransactionBuilder>` - TransactionBuilder which should be used in `Transaction.submitTransaction`.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_staking#example-4)

```typescript
const walletInfo = await Keypair.restoreFromPrivateKey(pkey, password);

// Define whether or not user desires to unstake all the tokens, or only part of the staked amount
const isFullUnstake = false;

const transactionBuilder = await StakingApi.unStake(
  walletInfo,
  amount,
  validator,
  isFullUnstake
);

const resultHandle = await Transaction.submitTransaction(transactionBuilder);y
```
