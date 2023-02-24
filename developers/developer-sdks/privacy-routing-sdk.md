---
description: Anonymous routing for every FRC20 transfer
---

# Privacy Routing SDK

### Introduction

`Privacy-Routing-SDK` provides simple and integration-friendly APIs for converting FRC20 transfers into anonymous transfers that break the link between senders and receivers. With just a small modification to your DApp's frontend, you can enhance your DeFi, Lending, or other project with privacy features.

### How It Works

`Privacy-Routing-SDK` is powered by zero-knowledge proof technology, allowing for the link between senders and receivers to be broken. The transfer can be completed in just four API calls&#x20;

1. **`depositFRC20()`** to deposit FRC20 tokens as a native asset in the ZK layer.
2. **`barToAbar()`** to wrap the native asset in an anonymous asset.
3. **`abarTobar()`** to unwrap the anonymous asset back to its native form.
4. **`barToEVM()`** to withdraw the native asset back to the EVM.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Note: In Findora's native chain, transparent assets are represented as **BAR**, while shielded assets are represented as **ABAR**.
{% endhint %}

The privacy routing process starts with funds being transferred from the sender's EVM address to the privacy layer for privacy shielding, and then back to the receiver's EVM address. During the privacy routing process, one-time receiver addresses are dynamically created and the asset passes through the privacy layer. The key steps are **`barToAbar()`** and **`abarTobar()`**, where the asset is wrapped and unwrapped using one-time stealth addresses, thereby breaking the link between the sender and receiver. The next version of the Privacy-Routing-SDK will simplify the process even further by consolidating multiple API calls into one or two calls to reduce complexity.

### Quickstart Tutorial

Developers can take a look at the `Privacy-Routing-SDK` example on Github.

{% embed url="https://github.com/FindoraNetwork/privacy-routing-sdk-example" %}

{% hint style="info" %}
Note: Privacy-Routing-SDK is now available only on the Findora **Forge** Testnet. See [network settings](../../network-settings/network-settings.md) for RPC details and request **Forge** EVM testnet `FRA` tokens [here](../../general-user-materials/acquire-fra/request-fra-testnet.md).
{% endhint %}

### DeFi Integration

The Findora `Privacy-Routing-SDK` is designed as a general tool for FRC20 tokens and can be integrated into various projects in different ways. In the context of DeFi, the simplest way to integrate the SDK is by adding it to the frontend without modifying the smart contracts.

As an example, let's consider **PancakeSwap** and a scenario where a user wants to swap 10 USDT to 9.98 USDC on the frontend page. The following are the adjusted steps for this scenario

**Step 1: Routing:**

* User address is: `0x661746C36C4379B5994d9883f3bFf662b711Be76`
* Call **`depositFRC20()`** to deposit 10 USDT as a native asset in the privacy layer.
* Call **`barToAbar()`** to wrap the native asset (10 USDT) in an anonymous asset.
* Call **`abarTobar()`** to unwrap the anonymous asset (10 USDT) back to its native form.
* Call **`barToEVM()`** to withdraw the native asset (10 USDT) back to an EVM one-time address.
* One-time receiver is: `0x7366F30D830048dFD947662d92421807bcB7Fdd3`

Upon completion of the privacy routing process, the link between the user address and the one-time receiver address holding 10 USDT is cut off.

**Step 2: Swap:**

* Switches to one-time receiver account: `0x7366F30D830048dFD947662d92421807bcB7Fdd3`.
* Performs a normal swap of 10 USDT to 9.98 USDC.
* Final receiver address doesn’t really matter. It could be the original user address `0x661746C36C4379B5994d9883f3bFf662b711Be76` , or it could be a different address.

The private swap is now complete.

### Simple Steps to Use

First [clone](https://github.com/FindoraNetwork/privacy-routing-sdk) and add the SDK to your project. You can also use package managers.

```bash
$ npm install privacy-routing-sdk
```

Copy [https://github.com/FindoraNetwork/wasm-js-bindings/tree/forge\_2022](https://github.com/FindoraNetwork/wasm-js-bindings/tree/forge\_2022) contents to \`external\_resources/findora-wallet-wasm\` in your project directory

* Download [Download ZIP](https://github.com/FindoraNetwork/wasm-js-bindings/archive/refs/heads/forge\_2022.zip)

`"findora-wallet-wasm": "./external_resources/findora-wallet-wasm"`&#x20;

in package.json. Example [https://github.com/FindoraNetwork/privacy-routing-sdk-example/tree/main/external\_resources/findora-wallet-wasm](https://github.com/FindoraNetwork/privacy-routing-sdk-example/tree/main/external\_resources/findora-wallet-wasm)

\


> **Import SDK**

```typescript
// Use appropriate ways to importing the privacy-routing-sdk
import { Sdk } from "privacy-routing-sdk";
const { Sdk } = require("privacy-routing-sdk");
```

> **Initiate SDK**

```typescript
import { Sdk } from "privacy-routing-sdk";

const ENV_CONFIG = {
  hostUrl: "findora RPC",
};

// Initiating the SDK configuration
await Sdk.init(ENV_CONFIG);
```

> **Forge Testnet Configuration**

{% code overflow="wrap" %}
```typescript
export const FINDORA_NETWORK = {
  chainId: 2154,
  chainName: 'Findora',
  nativeCurrency: {
    name: 'FRA',
    symbol: 'FRA',
    decimals: 18,
  },
  rpcUrls: ['https://prod-forge.prod.findora.org:8545'],
  blockExplorerUrls: ['https://prod-forge-blockscout.prod.findora.org/'],
};

export const CONTRACTS_ADDRESS = {
  simBridge: '0x893c29D3e6520466005C18683466136D73641201',
  prismBridge: '0x899d4d8f441E5B59EB21ceb58fce723bb5A85C55',
};

```
{% endcode %}

### The APIs

Generate the temp wallets for intermediate accounts,&#x20;

```typescript
// Wallets
const findoraWallets = await findora.keypair.getWallet();
const { walletStart, walletEnd, anonWallet } = findoraWallets;t
```



Using `Privacy-Routing-SDK` for a complete anonymous routing in 4 steps

*   **(1) Send assets From `Findora EVM` to `Findora Native Chain`**

    * Send **FRA** token to Findora Native Chain

    ```typescript
    await evm.transfer.fraToBar({
      bridgeAddress: simBridgeAddress, // bridge contract address
      recipientAddress: walletStart.address,     // wallet account address
      amount: "100", // amount in String
    });
    ```

    * Send **FRC20** token to Findora Native Chain

    {% code overflow="wrap" %}
    ```typescript
    /**
    Parameters
      bridgeAddress: simBridge contract address
      tokenAddress: FRC20 token address
      totalAmount: send amount
      recipientAddress: wallet account address
     */
    await evm.services.approveToken(tokenAddress, simBridgeAddress, tokenAmount);
    return await evm.transfer.frc20ToBar({
      bridgeAddress: simBridgeAddress,
      walletStart.address,
      tokenAddress, // 0x5b15Cdff7Fe65161C377eDeDc34A4E4E31ffb00B for zkUSDT on Forge testnet
      "100", // amount in String
    });

    // wait till the txn in successful and the assets converted
    // the first findora wallet should receive 3 utxo [asset, bar2abar_fee, bar2evm_fee]
          const { error: waitEvmToNativeUtxoError } = await findora.services.waitUtxoEnough(walletStart.publickey, 3);
          if (waitEvmToNativeUtxoError) throw waitEvmToNativeUtxoError;
    ```
    {% endcode %}




* **(2) Convert assets from `BAR` to `ABAR` in Findora Native Chain (entering anonymous cycle)**

```typescript
import { findora } from "privacy-routing-sdk";

// Fetch the converted asset Sids
// Sids are the index IDs of the UTXO in FRA chain
const { response: sids } = await findora.apis.getOwnedSids(walletStart.publickey);
/**
Parameters
  sids: consumable utxo sids
 */
const barToAbarResult =  await findora.transfer.barToAbar(
  walletWrap, // created earlier
  sids
);

if (barToAbarResult.txnLog) throw new Error(`barToAbar Error: ${barToAbarResult.txnLog}`);
console.log('barToAbar txnHash: ', barToAbarResult.txnHash);

// wait for 30 seconds
```

* **(3) Convert assets from `ABAR` to `BAR` in Findora Native Chain (leaving anonymous cycle)**

```typescript
import { findora } from "privacy-routing-sdk";

// commitments are the anonymous version of a private UTXO
// you can spend commitments owned by your anonWallet 
const commitments = barToAbarResult.commitments;

/**
Parameters
  commitments: consumable Abar utxo sids
 */
findora.transferabarToBar(
  walletWrap.anonWallet, // created earlier
  walletWrap.walletEnd,  // created earlier
  commitments
);
```

*   **(4) Withdraw assets from `Findora Native Chain` to `Findora EVM`**

    * Withdraw **FRA** token to Findora EVM

    ```typescript
    import { findora } from "privacy-routing-sdk";

    await findora.transfer.barToEVM(
      walletWrap.walletEnd, // created earlier
      "100", // amount
      recipientAddress, // recipient's EVM address
      "",
      "",
      false
    );
    ```

    * Withdraw **FRC20** token to Findora EVM

    {% code overflow="wrap" %}
    ```typescript
    import { findora, evm } from "privacy-routing-sdk";

    const assetCode = await evm.services.getAssetCode(
      prismBridgeAddress,
      tokenAddress, // FRC20 token address, 0x5b15Cdff7Fe65161C377eDeDc34A4E4E31ffb00B for zkUSDT on Forge testnet
      findoraNetworkRpcUrl // https://prod-forge.prod.findora.org:8545 for Forge testnet
    );

    await findora.transfer.barToEVM(
      walletWrap.walletEnd,
      "100", // amount
      recipientAddress, // recipient's address
      assetCode,
      "",
      false
    );
    ```
    {% endcode %}

### Boilerplate settings

```typescript
import { Sdk } from 'privacy-routing-sdk';
import Web3 from 'web3';

export const ENV_CONFIG = {
  hostUrl: 'https://prod-forge.prod.findora.org',
  feeServerUrl: 'https://forge.invisiblex.org/api/fee',
  configServerUrl: 'https://columbus-config.s3.us-west-2.amazonaws.com/columbus_config_forge.json',
  navticeExplorerUrl: 'https://forge.findorascan.io/',
};

export const FINDORA_EVM_CHAIN_ID = '2154';

Sdk.init({ ...ENV_CONFIG, web3: new Web3(Web3.givenProvider) });
```
