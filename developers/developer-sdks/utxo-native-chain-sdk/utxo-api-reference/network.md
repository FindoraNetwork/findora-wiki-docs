# Network



#### getAbciInfo[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getabciinfo) <a href="#getabciinfo" id="getabciinfo"></a>

_**- Get ABCI information**_\
This method is used to get ABCI information.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters)

* &#x20; `<string>` - a wallet address
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results)

* &#x20; `Promise<AbciInfoResult>` - An instance of `AbciInfoResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example)

```typescript
const data = "0x12345d";

// Get ABCI information
const acbiInfo = await Network.getAbciInfo(data);
```

#### getAbciNoce[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getabcinoce) <a href="#getabcinoce" id="getabcinoce"></a>

_**- Get ABCI Noce**_\
This method is used to get ABCI Noce.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-1)

* &#x20; `<string>` - a wallet address
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-1)

* &#x20; `Promise<AbciNoceResult>` - An instance of `AbciNoceResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-1)

```typescript
const data = "0x12345d";

// Get ABCI Noce
const acbiNoce = await Network.getAbciNoce(data);
```

#### getAssetToken[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getassettoken) <a href="#getassettoken" id="getassettoken"></a>

_**- Get information of given type of asset token**_\
This method is used to get information of given type of asset token

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-2)

* &#x20; `<string>` - asset code
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-2)

* &#x20; `Promise<AssetTokenDataResult>` - An instance of `AssetTokenDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-2)

```typescript
const data = "0x12345d";

// Get ABCI Noce
const acbiNoce = await Network.getAbciNoce(data);
```

#### getBlock[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getblock) <a href="#getblock" id="getblock"></a>

_**- Get datails of given block**_\
This method is used to get details of given block.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-3)

* &#x20; `<number>` - block Height
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-3)

* &#x20; `Promise<BlockDetailsDataResult>` - An instance of `BlockDetailsDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-3)

{% code overflow="wrap" %}
```typescript
const blockHeight = 1432;// Get block #1432 detailsconst blockDetail = await Network.getBlock(blockHeight);
```
{% endcode %}

#### getDelegateInfo[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getdelegateinfo) <a href="#getdelegateinfo" id="getdelegateinfo"></a>

_**- Get the delegation information**_\
This method is used to get the delegation information.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-4)

* &#x20; `<string>` - public key
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-4)

* &#x20; `Promise<DelegateInfoDataResult>` - An instance of `DelegateInfoDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-4)

{% code overflow="wrap" %}
```typescript
const publickey = "qsedx23rtgds";

// Get the delegation information
const blockDetail = await Network.getDelegateInfo(publickey);
```
{% endcode %}

#### getHashSwap[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#gethashswap) <a href="#gethashswap" id="gethashswap"></a>

_**- Get transaction details**_\
This method is used to get details of transaction with given hash

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-5)

* &#x20; `<string>` - transaction hash
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-5)

* &#x20; `Promise<HashSwapDataResult>` - An instance of `HashSwapDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-5)

```typescript
const hash = `YOUR_TX_HASH`;

// Get transaction details of given hash
const txDetail = await Network.getHashSwap(hash);
```

#### getIssuedRecords[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getissuedrecords) <a href="#getissuedrecords" id="getissuedrecords"></a>

_**- Get information of issued records for given public key**_\
This method is used to get information of issued records for given public key

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-6)

* &#x20; `<string>` - public key
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-6)

* &#x20; `Promise<IssuedRecordDataResult>` - An instance of `IssuedRecordDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-6)

```typescript
const publickey = `publickeyexample`;

// Get issed records information
const issuedRecords = await Network.getIssuedRecords(publickey);
```

#### getOwnedSids[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getownedsids) <a href="#getownedsids" id="getownedsids"></a>

_**- Get Sids owned by given address**_\
This method is used to get Sids owned by given address

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-7)

* &#x20; `<string>` - wallet address
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-7)

* &#x20; `Promise<OwnedSidsDataResult>` - An instance of `OwnedSidsDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-7)

```typescript
const address = `frabhhjsswerf`;

// Get Sids' information
const ownedSids = await Network.getOwnedSids(address);
```

#### getOwnerMemo[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getownermemo) <a href="#getownermemo" id="getownermemo"></a>

_**- Get the owner memo by given UTXO sid**_\
This method is used to get owner memo by given UTXO sid

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-8)

* &#x20; `<number>` - UTXO sid
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-8)

* &#x20; `Promise<OwnerMemoDataResult>` - An instance of `OwnerMemoDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-8)

```typescript
const utxoSid = 143;

// Get owner memo
const ownerMemo = await Network.getOwnerMemo(utxoSid);
```

#### getStateCommitment[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getstatecommitment) <a href="#getstatecommitment" id="getstatecommitment"></a>

_**- Returns state commitment**_\
An important property of a Findora ledger is the ability to authenticate transactions. Users can authenticate transactions against a small tag called the state commitment. The state commitment is a commitment to the current state of the ledger. The state commitment response is a tuple containing the state commitment and the state commitment version.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-9)

* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-9)

* &#x20; `Promise<StateCommitmentDataResult>` - An instance of `StateCommitmentDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-9)

```
// Get state commitment
const stateCommitment = await Network.getStateCommitment();
```

#### getTransactionStatus[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#gettransactionstatus) <a href="#gettransactionstatus" id="gettransactionstatus"></a>

_**- Returns transaction status**_\
Using the transaction handle, user can fetch the status of the transaction from the query server.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-10)

* &#x20; `<string>` - transaction handle (hash)
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-10)

* &#x20; `Promise<TransactionStatusDataResult>` - An instance of `TransactionStatusDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-10)

```typescript
const handle = `YOUR_TX_HASH`;

// Get transaction status
const transactionStatus = await Network.getTransactionStatus(handle);
```

#### getTransactionDetails[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#gettransactiondetails) <a href="#gettransactiondetails" id="gettransactiondetails"></a>

_**- Returns transaction details**_\
Using the transaction handle, user can fetch the details of the transaction from the query server.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-11)

* &#x20; `<string>` - transaction handle (hash)
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-11)

* &#x20; `Promise<TxDetailsDataResult>` - An instance of `TxDetailsDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-11)

```typescript
const handle = `YOUR_TX_HASH`;

// Get transaction details
const transactionDetails = await Network.getTransactionDetails(handle);
```

#### getTxList[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#gettxlist) <a href="#gettxlist" id="gettxlist"></a>

_**- Get a list of transactions for given wallet address**_\
This method is used to get a list of transactions for given wallet address

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-12)

* &#x20; `<string>` - wallet address
* &#x20; `<"to"|"from">` - transaction type. it can only be "to" or "from"
* &#x20; `<number>` - pagination. Default is 1.
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-12)

* &#x20; `Promise<TxListDataResult>` - An instance of `TxListDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-12)

```typescript
const address = `fra000xxsr`;
const type = "to";

// Get list of `to` transaction of given address
const txDetail = await Network.getTxList(address, type);
```

#### getUtxo[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getutxo) <a href="#getutxo" id="getutxo"></a>

_**- Get UTXO ledger for given utxo sid**_\
This method is used to get UTXO ledger for given UTXO sid

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-13)

* &#x20; `<number>` - UTXO SID
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-13)

* &#x20; `Promise<UtxoDataResult>` - An instance of `UtxoDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-13)

```typescript
const utxoSid = 143;

// Get UTXO details
const utxoData = await Network.getUtxo(utxoSid);
```

#### getValidatorList[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#getvalidatorlist) <a href="#getvalidatorlist" id="getvalidatorlist"></a>

_**- Get validator list**_\
This method is used to get the list of validators.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-14)

* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-14)

* &#x20; `Promise<ValidatorListDataResult>` - An instance of `ValidatorListDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-14)

```typescript
// Get validator list
const acbiInfo = await Network.getValidatorList();
```

#### sendRpcCall[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#sendrpccall) <a href="#sendrpccall" id="sendrpccall"></a>

_**- Send RPC call**_\
This method is used to send RPC call.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-15)

* &#x20; `<string>` - RPC url
* &#x20; `<{[key: string]: any}>` - payload
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-15)

* &#x20; `Promise<T>` - The response object from RPC call.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-15)

```typescript
cont url = `https://prod-testnet.prod.findora.org:8545`;
const payload = {
  method: `eth_getBlockByHash`,
  params: ['0x1af723767d06...',true],
};

// Send the RPC call to get block details by hash
const response = await Network.sendRpcCall(url,payload);
```

#### submitEvmTx[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#submitevmtx) <a href="#submitevmtx" id="submitevmtx"></a>

_**- Submit EVM transaction**_\
This method is used to submit a EVM transaction.

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-16)

* &#x20; `<string>` - transaction hash
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-16)

* &#x20; `Promise<SubmitEvmTxResult>` - An instance of `SubmitEvmTxResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-16)

```typescript
const tx = "Your_TX_Hash";

// Submit a EVM transaction
const result = await Network.submitEvmTx(tx);
```

#### submitTransaction[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#submittransaction) <a href="#submittransaction" id="submittransaction"></a>

_**- Submit transation**_\
This method is used to submit a transaction

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#parameters-17)

* &#x20; `<TransactionData>` - (optinal) transaction data
* &#x20; `<NetworkAxiosConfig>` - (optinal) network config

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#results-17)

* &#x20; `Promise<SubmitTransactionDataResult>` - An instance of `SubmitTransactionDataResult` containing the response and error.

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_network#example-17)

```typescript
const data = `Your_Transaction_Data`;

// Submit transaction
const txResult = await Network.submitTransaction(data);
```
