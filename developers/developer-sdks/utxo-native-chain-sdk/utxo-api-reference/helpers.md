# Helpers

#### getBlockTime[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#getblocktime) <a href="#getblocktime" id="getblocktime"></a>

_**- Get Block Time by given block height.**_\
Using this function, user can get block time by given block height

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#parameters)

* &#x20; `<number>` - block height

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#results)

* &#x20; `Promise<undefined | string>` - Block time

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#example)

```typescript
const blockHeight = 2341;
// Get block time at Block #2341
const blockTime = await helpers.getBlockTime(blockHeight);
```

#### getTxListFromResponse[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#gettxlistfromresponse) <a href="#gettxlistfromresponse" id="gettxlistfromresponse"></a>

_**- Get Transaction List by given transaction data response.**_\
Using this function, user can Get Transaction List by given transaction data response

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#parameters-1)

* &#x20; `<TxListDataResult>` - transaction data response

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#results-1)

* &#x20; `Promise<null | TxInfo[]>` - transaction list

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#example-1)

```typescript
const address = "fra12dsfew";
const type = "to";
const dataResult = await Network.getTxList(address, type);
// Get tx list
const txList = await helpers.getTxListFromResponse();
```

#### getTxOperationsList[​](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#gettxoperationslist) <a href="#gettxoperationslist" id="gettxoperationslist"></a>

_**- Get Operation List by given parsed transaction**_\
Using this function, user can Get Transaction List by given parsed transaction

**Parameters:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#parameters-2)

* &#x20; `<ParsedTx>` - parsed tx info

**Results:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#results-2)

* &#x20; `TxOperation[]>` - transaction operation list

**Example:**[**​**](https://wiki.findora.org/docs/developers/utxo/sdk-api/sdk\_api\_helpers#example-2)

```typescript
const address = "fra12dsfew";
const type = "to";
const dataResult = await Network.getTxList(address, type);
// Get tx list
const txList = await helpers.getTxListFromResponse();
// Get one parsed tx
parsedTx = JSON.parse(Base64.decode(txList[0].tx));
// Get operation Lsit
opList = helpers.getTxOperationsList(parsedTx);
```
